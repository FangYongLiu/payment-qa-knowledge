---
id: tbl_loyalty_t_cashback_transactions_2026_06
object_type: Table
name: Cashback reward transactions via Airdrop M2U API - 2026-06 (t_cashback_transactions_2026_06)
aliases: [t_cashback_transactions_2026_06, loyalty.t_cashback_transactions_2026_06]
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

# Cashback reward transactions via Airdrop M2U API - 2026-06 (t_cashback_transactions_2026_06)

## 用途
物理表 `loyalty.t_cashback_transactions_2026_06`,主键 `id`。Cashback reward transactions via Airdrop M2U API - 2026-06。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `user_id` | bigint unsigned | FK to t_users.id |
| `ucid` | varchar(50) | User UCID for M2U API |
| `campaign_id` | bigint unsigned | FK to t_campaigns.id · 可空 |
| `achievement_id` | bigint unsigned | FK to t_achievements.id · 可空 |
| `source_event_id` | varchar(100) | Event that triggered this cashback |
| `amount` | decimal(15, 2) | Cashback amount |
| `original_amount` | decimal(15, 2) | Talon-calculated amount before session-cap. NULL for historical rows pre-LOYAL-507. · 可空 |
| `currency` | char(3) | 待补 |
| `order_description` | varchar(100) | Order description for M2U API (user-visible in PayBy app) |
| `memo` | varchar(200) | Memo for M2U API (internal tracking) · 可空 |
| `biz_source` | varchar(200) | Business source for M2U API (categorizes transfer type) · 可空 |
| `status` | varchar(15) | Status: pending|processing|completed|failed|revoked |
| `cashdesk_request_id` | varchar(100) | Idempotency key (CB{t_custom_effects.id}) - set when API called · 可空 |
| `cashdesk_transaction_id` | varchar(100) | Transaction ID returned by M2U API · 可空 |
| `cashdesk_order_no` | varchar(100) | Order number from M2U (for callback matching) · 可空 |
| `cashdesk_status` | varchar(50) | Raw status from M2U: SETTLED, PENDING, SETTLING, REVOKED · 可空 |
| `failure_reason` | varchar(100) | 待补 · 可空 |
| `failure_code` | varchar(50) | Error code from M2U API · 可空 |
| `api_called_at` | timestamp | When M2U API was called · 可空 |
| `settled_at` | timestamp | When payment was settled · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_cashback_request_id`:cashdesk_request_id (UNIQUE)
- `idx_cashback_created`:created_at
- `idx_cashback_ucid_status`:ucid, status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
