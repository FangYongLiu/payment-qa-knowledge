---
id: tbl_acquireii_t_void_ops_order
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
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
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_void_ops_order` 记录由**运营人员**通过后台工具触发的收单撤销订单（ops = operations，运营撤销），与商户/用户主动发起撤销的 `t_void_order` 区分开。

典型场景：
- 异常订单需要运营人工介入撤销
- 测试订单的清理
- 风控拦截后的强制撤销

重要程度：⭐⭐⭐

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

关联：`acquire_global_id` → `t_acquire_order.global_id`（N:1）。

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_voo_aid` | `acquire_global_id` | 通过原订单查 |
| `i_voo_ct` | `created_time` | 按时间查 |
| `i_voo_lut` | `last_updated_time` | 按更新时间扫 |

## 校验点(QA 关注)

1. **运营撤销有审计要求**：通常需要双人复核。
2. **与 t_void_order 数据不重叠**：运营撤销不影响商户主动撤销，两张表分别承载不同来源的撤销记录，校验时不要混查。
3. **可能涉及强制状态修改**：异常订单清理场景下会强制改状态，需关注 `status`、`fail_code`、`fail_message`、`unity_result_code` 是否符合实际处置语义。
4. 通过 `acquire_global_id` 反查原订单时，应确保与 `t_acquire_order.global_id` 对应。
5. 常用查询：`SELECT * FROM t_void_ops_order WHERE acquire_global_id = ?;`，命中 `i_voo_aid`。
