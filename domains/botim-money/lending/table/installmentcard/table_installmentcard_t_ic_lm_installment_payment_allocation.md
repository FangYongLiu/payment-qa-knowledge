---
id: tbl_installmentcard_t_ic_lm_installment_payment_allocation
object_type: Table
name: Payment to installment allocation (t_ic_lm_installment_payment_allocation)
aliases: [t_ic_lm_installment_payment_allocation, installmentcard.t_ic_lm_installment_payment_allocation]
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

# Payment to installment allocation (t_ic_lm_installment_payment_allocation)

## 用途
物理表 `installmentcard.t_ic_lm_installment_payment_allocation`,主键 `id`。Payment to installment allocation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `account_id` | bigint | Account identifier (denormalized for queries, no FK) |
| `loan_id` | bigint | Loan identifier (logical ref to t_ic_lm_order.id, no FK) |
| `installment_id` | bigint | Installment identifier (logical ref to t_ic_lm_installment.id, no FK). NULL for payment-level allocations · 可空 |
| `payment_id` | bigint | Payment record (logical ref to t_ic_stl_payment.id, no FK) |
| `statement_id` | bigint | Statement identifier (logical ref to t_ic_stm_statement.id, no FK). NULL if before billing · 可空 |
| `allocated_amount` | decimal(18, 2) | Amount allocated (negative for reversals) |
| `allocation_type` | tinyint | Type: 0=NORMAL, 1=REVERSAL, 2=CHARGEBACK, 3=REFUND |
| `allocation_order` | int | Order within payment (1..N) |
| `idempotency_key` | varchar(100) | Unique key to prevent duplicate allocation |
| `allocated_at` | datetime | When allocation happened |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_idempotency_key`:idempotency_key (UNIQUE)
- `idx_account_id`:account_id
- `idx_installment_id`:installment_id
- `idx_loan_id`:loan_id
- `idx_statement_id`:statement_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
