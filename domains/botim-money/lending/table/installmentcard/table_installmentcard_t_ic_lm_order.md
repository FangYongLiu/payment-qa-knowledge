---
id: tbl_installmentcard_t_ic_lm_order
object_type: Table
name: Loan from captured transaction. 1 txn = 1 loan (t_ic_lm_order)
aliases: [t_ic_lm_order, installmentcard.t_ic_lm_order]
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

# Loan from captured transaction. 1 txn = 1 loan (t_ic_lm_order)

## 用途
物理表 `installmentcard.t_ic_lm_order`,主键 `id`。Loan from captured transaction. 1 txn = 1 loan。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key: internal loan identifier · 可空 |
| `account_id` | bigint | Account identifier (logical ref to t_ic_am_account.id, no FK) |
| `member_id` | varchar(32) | External member/customer identifier (optional, no FK) · 可空 |
| `source_txn_id` | bigint | Source captured transaction (logical ref to t_ic_cm_card_txn.id, unique, no FK) |
| `order_no` | varchar(32) | External order number: ICO + yyyyMMdd + 7-digit sequence (e.g. ICO202606050000167). Generated from leaf_alloc SEQ_IC_ORDER_NO at order creation. · 可空 |
| `product_id` | bigint | Product identifier (logical ref to t_ic_pm_product.id, no FK) |
| `product_version_id` | bigint | Product version (locks rules at loan creation, no FK) |
| `loan_amount` | decimal(18, 2) | Loan principal (= captured_amount from transaction) |
| `remaining_principal` | decimal(18, 2) | Outstanding principal after refund adjustments. Set to loan_amount at creation, reduced by principal settled from installments during refund. · 可空 |
| `total_interest_amount` | decimal(18, 2) | Total interest calculated at creation |
| `original_total_interest_amount` | decimal(18, 2) | Interest at loan creation (never updated by refunds) · 可空 |
| `irr` | decimal(10, 6) | Internal Rate of Return (annualized rate for disclosure) · 可空 |
| `currency` | varchar(3) | Currency (ISO 4217, e.g., AED) |
| `tenure_months` | int | Loan tenure (MVP: 4; Future: user-selected 3/6/9/12) |
| `loan_status` | tinyint | Status: 0=CREATED, 1=ACTIVE, 2=CLOSED, 3=CANCELLED, 4=DEFAULTED |
| `closure_reason` | tinyint | 0=NORMAL, 1=REFUND, 2=EARLY_SETTLEMENT · 可空 |
| `fine` | int | fine applied |
| `fee` | int | fee applied |
| `start_date` | date | Loan schedule start date |
| `closed_at` | datetime | When loan was closed/completed · 可空 |
| `cancelled_at` | datetime | When loan was cancelled (refund/reversal) · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_order_no`:order_no (UNIQUE)
- `uk_source_txn_id`:source_txn_id (UNIQUE)
- `idx_account_status`:account_id, loan_status
- `idx_member_id`:member_id
- `idx_start_date`:start_date

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
