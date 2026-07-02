---
id: tbl_installmentcard_t_ic_lm_installment
object_type: Table
name: Installment obligations. MVP: 4 per loan (t_ic_lm_installment)
aliases: [t_ic_lm_installment, installmentcard.t_ic_lm_installment]
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

# Installment obligations. MVP: 4 per loan (t_ic_lm_installment)

## 用途
物理表 `installmentcard.t_ic_lm_installment`,主键 `id`。Installment obligations. MVP: 4 per loan。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key: internal installment identifier · 可空 |
| `loan_id` | bigint | Loan identifier (logical ref to t_ic_lm_order.id, no FK) |
| `account_id` | bigint | Account identifier (denormalized for queries, no FK) |
| `installment_no` | int | Installment sequence (MVP: 1-4; Future: 1-N based on tenure) |
| `due_date` | date | Installment due date |
| `principal_amount` | decimal(18, 2) | Principal component |
| `interest_amount` | decimal(18, 2) | Interest component (PRD: IRR-based calculation) |
| `opening_balance` | decimal(18, 2) | Principal balance at start of installment (before this payment) |
| `closing_balance` | decimal(18, 2) | Principal balance at end of installment (after principal payment) |
| `fee_amount` | decimal(18, 2) | Fee component due |
| `fine_amount` | decimal(18, 2) | Fine/penalty due |
| `due_amount` | decimal(18, 2) | Total due = principal + interest + fee + fine |
| `currency` | varchar(3) | Currency (ISO 4217, e.g., AED) |
| `billing_status` | tinyint | Billing status: 0=UNBILLED, 1=BILLED |
| `payment_status` | tinyint | Payment status: 0=NOT_DUE, 1=DUE, 2=PAID, 3=OVERDUE, 4=PARTIAL, 5=CANCELLED, 6=WAIVED |
| `paid_amount` | decimal(18, 2) | Total paid (sum of allocations) |
| `outstanding_amount` | decimal(18, 2) | Remaining unpaid (initially = due_amount) |
| `paid_principal_amount` | decimal(18, 2) | Paid principal (sum of allocations to principal) |
| `paid_interest_amount` | decimal(18, 2) | Paid interest (sum of allocations to interest) |
| `paid_fee_amount` | decimal(18, 2) | Paid fee (sum of allocations to fee) |
| `paid_fine_amount` | decimal(18, 2) | Paid fine/penalty (sum of allocations to fine) |
| `statement_id` | bigint | Statement where billed (logical ref to t_ic_stm_statement.id, no FK) · 可空 |
| `billed_at` | datetime | When added to statement · 可空 |
| `paid_at` | datetime | When fully paid · 可空 |
| `waived_at` | datetime | When waived (if applicable) · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_account_id`:account_id
- `idx_loan_id`:loan_id
- `idx_statement_id`:statement_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
