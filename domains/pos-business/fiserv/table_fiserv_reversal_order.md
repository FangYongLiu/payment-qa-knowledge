---
id: tbl_fiserv_reversal_order
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_fiserv_reversal_order.md
tags:
- fiserv
- reversal
- 冲正
subdomain: fiserv
module: null
sensitivity: normal
name: Fiserv Reversal订单表
aliases:
- t_fiserv_reversal_order
- acquireii.t_fiserv_reversal_order
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

Fiserv 渠道的 **reversal（反向冲账）订单表** `acquireii.t_fiserv_reversal_order`。当 Fiserv 接口通信异常时，需要发送 reversal 报文冲销原交易，本表记录每次 reversal 请求及其重发与状态。重要程度 ⭐⭐⭐。

## 关键列

### 主键与关联
- `global_id` bigint ✅ — 主键
- `request_no` varchar(200) ✅ — 请求 No
- `mis_order_no` varchar(200) — mis 订单号
- `origin_global_id` bigint ✅ — 原始订单号（关联 `t_fiserv_sale_order.global_id`）
- `type` varchar(32) ✅ — 冲正类型（区分协议层 / 业务层 reversal）
- `retransmission` int ✅ — 重发计数

### 业务方
- `device_id` varchar(200) ✅ — 设备 ID
- `partner_id` varchar(32) ✅ — 商户 ID

### Fiserv 渠道
- `res_payload_token` varchar(32) — 响应负载 Token
- `channel_param_id` bigint — 渠道参数 ID
- `current_cmd_id` bigint — 当前指令 ID

### 状态机
- `status` varchar(50) ✅ — 状态（如 `FAILED`）
- `fail_code` varchar(50) — 错误码
- `fail_message` varchar(200) — 错误描述
- `unity_result_code` varchar(200) — 统一结果码

### 时间与版本
- `created_time` timestamp(3) ✅
- `last_updated_time` timestamp(3) ✅
- `data_version` bigint ✅

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_fro_oid` | `origin_global_id` | 通过原订单查 reversal |
| `i_fro_rn` | `request_no` | 按 request_no 查 |
| `i_fro_ct` | `created_time` | 按创建时间查 |
| `i_fro_lut` | `last_updated_time` | 按更新时间查 |

关联：`t_fiserv_sale_order` N:1，`origin_global_id → global_id`。

## 校验点(QA 关注)

1. **失败的 reversal 是资金风险**：`status = 'FAILED'` 且 `retransmission >= 3` 必须告警，人工跟进。参考查询：
   ```sql
   SELECT global_id, origin_global_id, retransmission, fail_message, created_time
   FROM t_fiserv_reversal_order
   WHERE status = 'FAILED' AND retransmission >= 3
   ORDER BY created_time DESC;
   ```
2. **retransmission 重发次数**：监控是否超过阈值，超过需人工介入。
3. **type 冲正类型**：校验协议层 reversal 与业务层 reversal 的区分是否正确。
4. **origin_global_id 必须能在 `t_fiserv_sale_order` 找到对应原单**，否则为孤立 reversal。
5. **fail_code / fail_message / unity_result_code** 在失败场景下应非空，便于排障。
