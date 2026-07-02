---
id: tbl_installmentcard_t_ic_am_overlimit_event
object_type: Table
name: Tracks overlimit events for fee calculation at statement generation (t_ic_am_overlimit_event)
aliases: [t_ic_am_overlimit_event, installmentcard.t_ic_am_overlimit_event]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Tracks overlimit events for fee calculation at statement generation (t_ic_am_overlimit_event)

## 用途
物理表 `installmentcard.t_ic_am_overlimit_event`,主键 `id`。Tracks overlimit events for fee calculation at statement generation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `account_id` | bigint | Account identifier (logical ref to t_ic_am_account.id, no FK) |
| `trigger_txn_id` | bigint | Transaction that triggered overlimit (logical ref to t_ic_cm_card_txn.id, no FK). NULL if caused by limit decrease · 可空 |
| `trigger_type` | tinyint | Trigger type: 0=CLEARING_EXCEEDED, 1=LIMIT_DECREASE, 2=FORCE_SETTLEMENT |
| `overlimit_amount` | decimal(18, 2) | Amount over the credit limit |
| `credit_limit_at_event` | decimal(18, 2) | Credit limit at time of event |
| `used_limit_at_event` | decimal(18, 2) | Used limit at time of event |
| `event_status` | tinyint | Status: 0=ACTIVE, 1=RESOLVED, 2=FEE_APPLIED |
| `resolved_at` | datetime | When overlimit was resolved (balance normalized) · 可空 |
| `fee_statement_id` | bigint | Statement where overlimit fee was applied (logical ref to t_ic_stm_statement.id, no FK) · 可空 |
| `created_at` | datetime | Event timestamp |
| `updated_at` | datetime | Last update |

## 主键 / 索引
- 主键:`id`
- `idx_account_status`:account_id, event_status
- `idx_created_at`:created_at
- `idx_trigger_txn`:trigger_txn_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
