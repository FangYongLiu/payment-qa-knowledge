---
id: tbl_acquireii_t_void_ops_order
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_void_ops_order.md
tags:
- 撤销
- 运营
- acquireii
subdomain: acquireii
module: void
sensitivity: normal
name: 运营撤销订单表
aliases:
- t_void_ops_order
- voidops订单
related_services:
- svc_acquireii
---

## 用途

`acquireii.t_void_ops_order` 记录由**运营人员**通过后台工具触发的收单撤销订单（ops = operations，运营撤销），与商户/用户主动发起的撤销表 `t_void_order` 区分开，分别承载不同来源的撤销记录。

典型场景：
- 异常订单需要运营人工介入撤销
- 测试订单的清理
- 风控拦截后的强制撤销

重要程度：⭐⭐⭐

## 在交易链路中的位置

收单链路（简化）：

```
t_acquire_order（原收单订单）
  ├── t_void_order         ← 商户/用户主动撤销
  ├── t_void_ops_order     ← 运营后台撤销（本表）
  ├── t_reversal_order     ← Reversal
  ├── t_revoke_order       ← 冲正
  └── t_refund_order       ← 退款
```

本表是**运营侧撤销**的落库点，不参与正常商户交易链路，仅在人工/风控/清理场景下产生记录。撤销动作通常通过 `t_command` / 渠道参数（`t_channel_param`）下发到上游渠道。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `global_id` | bigint | ✅ | 主键，全局号 |
| `merchant_order_no` | varchar(200) | ✅ | 商户订单号（request_no） |
| `acquire_global_id` | bigint | ✅ | 原收单订单号 |
| `channel_param_id` | bigint |  | 渠道参数 ID |
| `partner_id` | varchar(200) | ✅ | 发起方 memberId |
| `device_id` | varchar(200) |  | 设备号 |
| `status` | varchar(32) | ✅ | 撤销状态 |
| `mis_order_no` | varchar(128) |  | mis 订单号 |
| `fail_code` | varchar(50) |  | 错误码 |
| `fail_message` | varchar(200) |  | 错误描述 |
| `unity_result_code` | varchar(200) |  | 统一结果码 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本 |

## 关联关系

| 字段 | 关联表 | 关系 | 说明 |
|------|--------|------|------|
| `acquire_global_id` | `t_acquire_order.global_id` | N:1 | 反查原收单订单 |
| `channel_param_id` | `t_channel_param` | N:1 | 撤销使用的渠道参数 |
| `merchant_order_no` | 业务请求号 | — | 与 `t_acquire_order.request_no` 体系一致 |
| 同 `acquire_global_id` | `t_void_order` | 互斥 | 商户主动撤销与运营撤销不应同时存在/混查 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_voo_aid` | `acquire_global_id` | 通过原订单查 |
| `i_voo_ct` | `created_time` | 按时间查 |
| `i_voo_lut` | `last_updated_time` | 按更新时间扫 |

## QA 落库检查要点

1. **来源区分**：运营撤销落 `t_void_ops_order`，商户/用户主动撤销落 `t_void_order`，两表数据不重叠，检查脚本不要混查同一笔单。
2. **审计要求**：运营撤销通常需要双人复核，QA 在端到端测试时关注后台审批链路与本表落库时间是否一致。
3. **强制状态修改**：异常订单清理可能强制改状态，需重点校验 `status`、`fail_code`、`fail_message`、`unity_result_code` 是否符合实际处置语义。
4. **原单一致性**：通过 `acquire_global_id` 反查 `t_acquire_order.global_id` 必须命中，且原单状态应允许撤销。
5. **partner_id 一致性**：`partner_id` 应与原收单订单的发起方 memberId 对齐。
6. **常用查询**：
   ```sql
   SELECT * FROM t_void_ops_order WHERE acquire_global_id = ?;  -- 命中 i_voo_aid
   SELECT * FROM t_void_ops_order WHERE merchant_order_no = ?;
   ```
7. **失败语义**：当 `status` 为失败态时，`fail_code` / `fail_message` / `unity_result_code` 三者应同时存在并语义一致。
