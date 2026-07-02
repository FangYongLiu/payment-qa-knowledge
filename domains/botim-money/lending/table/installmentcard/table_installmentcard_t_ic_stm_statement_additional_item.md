---
id: tbl_installmentcard_t_ic_stm_statement_additional_item
object_type: Table
name: Statement additional activity items (repayments, refunds) (t_ic_stm_statement_additional_item)
aliases: [t_ic_stm_statement_additional_item, installmentcard.t_ic_stm_statement_additional_item]
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

# Statement additional activity items (repayments, refunds) (t_ic_stm_statement_additional_item)

## 用途
物理表 `installmentcard.t_ic_stm_statement_additional_item`,主键 `id`。Statement additional activity items (repayments, refunds)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `statement_id` | bigint | logical ref to installmentcard.t_ic_stm_statement.id, no FK |
| `account_id` | bigint | logical ref to installmentcard.t_ic_am_account.id, no FK |
| `item_type` | tinyint | Activity type: 0=REPAYMENT, 1=REFUND |
| `ref_id` | bigint | Source row id (t_ic_pm_payment.id for REPAYMENT, t_ic_cm_card_txn.id for REFUND) |
| `amount` | decimal(18, 2) | Activity amount, always positive — sign is implied by item_type |
| `currency` | char(3) | ISO 4217 currency code |
| `activity_date` | timestamp | Activity date |
| `posting_date` | timestamp | Posting date |
| `original_transaction_id` | varchar(64) | REFUND only — original transaction id · 可空 |
| `merchant_name` | varchar(128) | REFUND only — merchant name · 可空 |
| `idempotency_key` | varchar(64) | Stable dedup key, "<TYPE>:<ref_id>" (e.g. REPAYMENT:12345) |
| `created_at` | timestamp | Row created time |
| `updated_at` | timestamp | Row updated time |

## 主键 / 索引
- 主键:`id`
- `uk_idempotency_key`:idempotency_key (UNIQUE)
- `idx_account_id`:account_id
- `idx_statement_id`:statement_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
