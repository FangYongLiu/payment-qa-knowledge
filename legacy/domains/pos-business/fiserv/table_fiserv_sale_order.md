---
id: tbl_fiserv_sale_order
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_fiserv_sale_order.md
tags:
- Fiserv
- 销售订单
- 核心交易表
subdomain: fiserv
module: null
sensitivity: normal
name: Fiserv销售订单表
aliases:
- t_fiserv_sale_order
- acquireii.t_fiserv_sale_order
related_services: []
related_tables:
- tbl_fiserv_batch
- tbl_fiserv_refund_order
- tbl_fiserv_reversal_order
- tbl_fiserv_sale_void_ops_order
- tbl_hardware_info
- tbl_merchant_device
- tbl_pos_settlement
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_payment_code_scanned_by_pos
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

Fiserv 渠道下的**销售订单**核心交易表，记录通过 Fiserv 渠道发起的 PURCHASE 类交易主单。它是 Fiserv 收单交易链路的中心表，与通用 `t_acquire_order` 相对应，但专属 Fiserv 渠道。

- 表名：`acquireii.t_fiserv_sale_order`
- 主键：`global_id`
- 重要程度：⭐⭐⭐⭐⭐

## 在交易链路中的位置

```
设备激活 (tbl_active_code / tbl_merchant_device)
        ↓
开批次 (tbl_fiserv_batch)        ← 必须先存在,否则不允许交易
        ↓
销售下单 (tbl_fiserv_sale_order) ← 本表,PURCHASE 主单
        ↓
  ┌─────┴─────┬──────────────┬────────────────┐
退款           撤销            冲正             结算
refund_order  void_ops_order  reversal_order   pos_settlement
```

本表是 Fiserv 渠道交易落库的入口,后续的退款/撤销/冲正/结算都通过 `global_id` 反查到原销售单。

## 关键列

### 主键和标识
- `global_id` bigint ✅ 主键,全局号
- `request_no` varchar(200) ✅ 请求 No(幂等键)
- `mis_order_no` varchar(200) MIS 订单号
- `rcpt_tx_id` varchar(50) 收据交易 ID(收据上的交易号,用户拿回来对账用)
- `type` varchar(50) 类型(默认 PURCHASE,可能还有其他类型)

### 业务方
- `device_id` varchar(200) ✅ 设备 ID(对应 `tbl_hardware_info` / `tbl_merchant_device`)
- `partner_id` varchar(32) ✅ 商户 ID

### Fiserv 渠道
- `res_payload_token` varchar(32) 响应负载 Token
- `channel_param_id` bigint 渠道参数 ID(关联 `t_fiserv_channel_param`)
- `current_cmd_id` bigint 当前指令 ID

### 状态机
- `status` varchar(50) ✅ 订单状态
- `fail_code` varchar(50) 错误码
- `fail_message` varchar(200) 错误描述
- `unity_result_code` varchar(200) 统一结果码

### 时间和版本
- `created_time` timestamp(3) ✅ 创建时间
- `last_updated_time` timestamp(3) ✅ 最后更新时间
- `data_version` bigint ✅ 数据版本(乐观锁)

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `i_fso_rn` | request_no | 按 request_no 查(幂等查询) |
| `i_fso_txid` | rcpt_tx_id | 按收据交易 ID 查(对账) |
| `i_fso_cci` | current_cmd_id | 按指令 ID 查 |
| `i_fso_ct` | created_time | 按时间查 |
| `i_fso_lut` | last_updated_time | 按更新时间查 |

## 关联表

| 关联表 | 关系 | 关联字段 | 说明 |
|--------|------|---------|------|
| `tbl_fiserv_batch` | N:1 | device_id | 交易必须发生在已开启批次内 |
| `tbl_fiserv_refund_order` | 1:N | global_id → origin_global_id | 退款单回链销售单 |
| `t_fiserv_refund_bucket` | 1:1 | global_id | 退款桶(汇总可退余额) |
| `tbl_fiserv_sale_void_ops_order` | 1:N | global_id → origin_global_id | 撤销单回链销售单 |
| `tbl_fiserv_reversal_order` | 1:N | global_id → origin_global_id | 冲正单回链销售单 |
| `t_fiserv_channel_param` | N:1 | channel_param_id | 渠道参数(含金额等) |
| `tbl_merchant_device` | N:1 | device_id + partner_id | 商户-设备绑定关系 |
| `tbl_pos_settlement` | N:1 | 通过批次/设备 | 销售单最终归入结算 |

## 校验点 (QA 关注)

### 落库检查要点
1. **金额信息不在这张表**:在 `t_payment_info` 或 `channel_param` 中,验金额需联查。
2. **type 默认 PURCHASE**:可能还有其他类型,断言时注意区分。
3. **rcpt_tx_id 是收据上的交易号**:用户拿回来对账时使用,应非空且唯一。
4. **必须先有 `tbl_fiserv_batch`**:设备必须先开批次才能交易,否则销售单不应落库或应为失败态。
5. **status 终态**:成功时应为 `SUCCESS`;失败时 `fail_code` / `fail_message` / `unity_result_code` 应有值。
6. **request_no 幂等**:相同 request_no 重复请求应返回同一 global_id。
7. **channel_param_id 必填**:Fiserv 交易必须绑定有效渠道参数。

### 常用查询场景
- 查询设备某天的所有交易:`device_id` + `DATE(created_time)`
- Fiserv 交易成功率统计:`status = 'SUCCESS'` 按近 7 天聚合
- 按收据号反查交易:走 `i_fso_txid` 索引
- 按 request_no 查幂等:走 `i_fso_rn` 索引
- 联查退款/撤销/冲正:用 `global_id` 反查对应表的 `origin_global_id`
