---
id: tbl_loyalty_t_gold_reward_transactions_2026_12
object_type: Table
name: Gold/Silver reward transactions lifecycle - 2026-12 (t_gold_reward_transactions_2026_12)
aliases: [t_gold_reward_transactions_2026_12, loyalty.t_gold_reward_transactions_2026_12]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: loyalty schema DDL
tags: [marketing, loyalty]
sensitivity: normal
related_services: []
---

# Gold/Silver reward transactions lifecycle - 2026-12 (t_gold_reward_transactions_2026_12)

## 用途
物理表 `loyalty.t_gold_reward_transactions_2026_12`,主键 `id`。Gold/Silver reward transactions lifecycle - 2026-12。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `request_order_no` | varchar(100) | Idempotency key sent to Gold Service: LOYALTY_GOLD_{YYYY_MM}_{id} or LOYALTY_SILVER_{YYYY_MM}_{id} |
| `event_id` | varchar(100) | Talon effect id for ingestion idempotency. NULL for admin-batch rows. · 可空 |
| `user_id` | bigint unsigned | FK to t_users.id |
| `ucid` | varchar(50) | Botim ucid; sent as receiver.uid to Gold Service |
| `campaign_id` | bigint unsigned | FK to t_campaigns.id. NULL for admin-batch rows. · 可空 |
| `achievement_id` | bigint unsigned | FK to t_achievements.id. NULL for admin-batch rows. · 可空 |
| `asset` | varchar(10) | gold | silver |
| `amount_mode` | varchar(10) | aed | grams — original reward denomination |
| `amount_aed` | decimal(15, 2) | AED value. Populated at insert when amount_mode=aed; from Gold Service Order.amount on success or permanent-fail when amount_mode=grams. · 可空 |
| `amount_grams` | decimal(18, 8) | Gram quantity. Populated at insert when amount_mode=grams; from Order.quantity on success when amount_mode=aed. · 可空 |
| `state` | varchar(20) | pending | waiting | success | cashback_issued | not_rewarded |
| `waiting_reason` | varchar(30) | kyc_consent | gold_service_pending. NULL outside waiting. · 可空 |
| `terminal_reason` | varchar(50) | Diagnostic for terminal states: adv_kyc_required, retry_exhausted, kyc_consent_timeout, etc. · 可空 |
| `consent_deadline_at` | timestamp | expireTime sent to Gold Service. Set on entry to waiting:kyc_consent. · 可空 |
| `retry_count` | int unsigned | Retry attempts so far |
| `next_retry_at` | timestamp | Next retry deadline for the retry-pending worker · 可空 |
| `last_error` | varchar(500) | Last Gold Service error code + message · 可空 |
| `gold_service_order_no` | varchar(100) | Order.order_id from Gold Service. Set on success. · 可空 |
| `fallback_txn_id` | bigint unsigned | FK to t_cashback_transactions_*.id when state=cashback_issued · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_gold_reward_request_order_no`:request_order_no (UNIQUE)
- `idx_gold_reward_state_retry`:state, next_retry_at
- `idx_gold_reward_ucid_state`:ucid, state

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
