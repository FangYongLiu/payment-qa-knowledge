---
id: tbl_fiserv_sale_order
object_type: Table
domain: device-pos
status: active
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

Fiserv 渠道下的**销售订单**核心交易表（PURCHASE 类型为主）。与通用 `t_acquire_order` 相对应，但专属 Fiserv 渠道。

- 表名：`acquireii.t_fiserv_sale_order`
- 主键：`global_id`
- 重要程度：⭐⭐⭐⭐⭐

## 关键列

### 主键和标识
- `global_id` bigint ✅ 主键，全局号
- `request_no` varchar(200) ✅ 请求 No
- `mis_order_no` varchar(200) mis 订单号
- `rcpt_tx_id` varchar(50) 收据交易 ID（收据上的交易号，用户拿回来对账用）
- `type` varchar(50) 类型（默认 PURCHASE，可能还有其他类型）

### 业务方
- `device_id` varchar(200) ✅ 设备 ID
- `partner_id` varchar(32) ✅ 商户 ID

### Fiserv 渠道
- `res_payload_token` varchar(32) 响应负载 Token
- `channel_param_id` bigint 渠道参数 ID
- `current_cmd_id` bigint 当前指令 ID

### 状态机
- `status` varchar(50) ✅ 订单状态
- `fail_code` varchar(50) 错误码
- `fail_message` varchar(200) 错误描述
- `unity_result_code` varchar(200) 统一结果码

### 时间和版本
- `created_time` timestamp(3) ✅ 创建时间
- `last_updated_time` timestamp(3) ✅ 最后更新时间
- `data_version` bigint ✅ 数据版本

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |
| `i_fso_rn` | request_no | 按 request_no 查 |
| `i_fso_txid` | rcpt_tx_id | 按收据交易 ID 查 |
| `i_fso_cci` | current_cmd_id | 按指令 ID 查 |
| `i_fso_ct` | created_time | 按时间查 |
| `i_fso_lut` | last_updated_time | 按更新时间查 |

### 关联表

| 关联表 | 关系 | 关联字段 |
|--------|------|---------|
| `t_fiserv_refund_order` | 1:N | global_id → origin_global_id |
| `t_fiserv_refund_bucket` | 1:1 | global_id |
| `t_fiserv_sale_void_ops_order` | 1:N | global_id → origin_global_id |
| `t_fiserv_reversal_order` | 1:N | global_id → origin_global_id |
| `t_fiserv_channel_param` | 1:N | global_id |
| `t_fiserv_batch` | N:1 | device_id |

## 校验点(QA 关注)

1. **金额信息不在这张表**：在 `t_payment_info` 或 `channel_param` 中。
2. **type 默认 PURCHASE**：可能还有其他类型，需注意区分。
3. **rcpt_tx_id 是收据上的交易号**：用户拿回来对账时使用。
4. **必须先有 `t_fiserv_batch`**：设备必须先开批次才能交易。
5. 常用查询场景：
   - 查询设备某天的所有交易（按 `device_id` + `DATE(created_time)`）。
   - Fiserv 交易成功率统计（按 `status = 'SUCCESS'` 统计近 7 天）。
