---
id: tbl_fiserv_reversal_order
object_type: Table
domain: device-pos
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
related_tables:
- tbl_fiserv_batch
- tbl_fiserv_refund_order
- tbl_fiserv_sale_order
- tbl_fiserv_sale_void_ops_order
related_scenarios:
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

Fiserv 渠道的 **reversal（反向冲账）订单表** `acquireii.t_fiserv_reversal_order`。当 Fiserv 接口通信异常（超时、连接断开、未明确响应等）时，需要发送 reversal 报文冲销原交易，避免对账方与本地资金状态不一致。本表记录每次 reversal 请求、重发次数及其最终状态。重要程度 ⭐⭐⭐（资金风险高）。

## 在交易链路中的位置

```
业务请求 (sale / void / refund)
   │
   ▼
t_fiserv_sale_order / t_fiserv_sale_void_ops_order / t_fiserv_refund_order  (原单)
   │  发卡组织通信异常 → 不确定原交易是否成功
   ▼
t_fiserv_reversal_order  ← 本表（通过 origin_global_id 关联原单）
   │  发送 reversal 冲销 → 重发直至成功或人工介入
   ▼
原单状态被冲正 / 资金回退
```

reversal 是 POS/Fiserv 链路的兜底机制：原单可能已在 Fiserv 侧落地、也可能未落地，必须通过 reversal 报文使两侧最终一致。

## 关键列

### 主键与关联
- `global_id` bigint ✅ — 主键
- `request_no` varchar(200) ✅ — 请求 No（幂等键）
- `mis_order_no` varchar(200) — mis 订单号
- `origin_global_id` bigint ✅ — 原始订单号（关联 `t_fiserv_sale_order.global_id` 等原单表）
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
- `status` varchar(50) ✅ — 状态（如 `FAILED`、`SUCCESS` 等）
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
| `i_fro_rn` | `request_no` | 按 request_no 查（幂等校验） |
| `i_fro_ct` | `created_time` | 按创建时间查 |
| `i_fro_lut` | `last_updated_time` | 按更新时间查 |

## 与其他表的关系

| 关联表 | 关系 | 关联键 | 说明 |
|--------|------|--------|------|
| `t_fiserv_sale_order` | N:1 | `origin_global_id → global_id` | 销售单 reversal |
| `t_fiserv_sale_void_ops_order` | N:1 | `origin_global_id → global_id` | 撤销操作 reversal |
| `t_fiserv_refund_order` | N:1 | `origin_global_id → global_id` | 退款 reversal |
| `t_fiserv_batch` | 间接 | 通过原单 batch_id | 批次结算时需排除 reversal 失败的原单 |

## QA 落库检查要点

1. **失败的 reversal 是资金风险**：`status = 'FAILED'` 且 `retransmission >= 3` 必须告警，人工跟进。参考查询：
   ```sql
   SELECT global_id, origin_global_id, retransmission, fail_message, created_time
   FROM t_fiserv_reversal_order
   WHERE status = 'FAILED' AND retransmission >= 3
   ORDER BY created_time DESC;
   ```
2. **retransmission 重发次数**：监控是否超过阈值（默认 3 次），超过需人工介入；正常成功的 reversal `retransmission` 应较小。
3. **type 冲正类型**：校验协议层 reversal（通信异常触发）与业务层 reversal（业务校验失败触发）的区分是否正确。
4. **origin_global_id 必须能在原单表（`t_fiserv_sale_order` 等）找到对应原单**，否则为孤立 reversal，需排查写入逻辑：
   ```sql
   SELECT r.global_id, r.origin_global_id
   FROM t_fiserv_reversal_order r
   LEFT JOIN t_fiserv_sale_order s ON r.origin_global_id = s.global_id
   WHERE s.global_id IS NULL;
   ```
5. **fail_code / fail_message / unity_result_code** 在失败场景下应非空，便于排障；成功场景下可为空。
6. **request_no 幂等**：同一 `request_no` 不应重复落库（应通过 `i_fro_rn` 唯一定位），重发应体现在 `retransmission` 自增而非新增行。
7. **原单状态一致性**：reversal 成功后，原单（`t_fiserv_sale_order` 等）状态应被同步冲正，避免出现「reversal 已 SUCCESS 但原单仍为 SUCCESS」的不一致。
8. **结算排除**：参与 `t_fiserv_batch` 结算前，应排除已被 reversal 成功冲销的原单，避免重复入账。
