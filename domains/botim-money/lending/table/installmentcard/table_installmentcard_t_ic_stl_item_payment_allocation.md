---
id: tbl_installmentcard_t_ic_stl_item_payment_allocation
object_type: Table
name: Payment to statement item allocation (t_ic_stl_item_payment_allocation)
aliases: [t_ic_stl_item_payment_allocation, installmentcard.t_ic_stl_item_payment_allocation]
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

# Payment to statement item allocation (t_ic_stl_item_payment_allocation)

## 用途
物理表 `installmentcard.t_ic_stl_item_payment_allocation`,主键 `id`。Payment to statement item allocation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `payment_id` | bigint | Logical ref to t_ic_stl_payment.id (no FK) |
| `account_id` | bigint | Logical ref to t_ic_am_account.id (no FK). Denormalized for filtering |
| `statement_id` | bigint | Statement ID — NULL if unbilled · 可空 |
| `statement_item_id` | bigint | Statement item ID — NULL if unbilled or wallet · 可空 |
| `early_settlement_id` | bigint | FK to t_ic_stl_early_settlement — set when paid via early settlement · 可空 |
| `early_settlement_loan_id` | bigint | FK to t_ic_stl_early_settlement_loan — set when paid via early settlement · 可空 |
| `settlement_type` | tinyint | 0=STATEMENT, 1=EARLY_SETTLEMENT · 可空 |
| `item_type` | tinyint | 0=PRINCIPAL, 1=INTEREST, 2=FEE, 3=FEE_VAT, 4=LPF, 5=LPF_VAT, 6=PREVIOUS_BALANCE, 7=WALLET_REFUND · 可空 |
| `refund_transfer_id` | bigint | FK to t_ic_pb_refund_transfer — set when payment is refunded to wallet · 可空 |
| `allocated_amount` | decimal(18, 2) | Amount allocated to statement item (negative for reversals) |
| `allocation_type` | tinyint | Allocation type: 0=NORMAL, 1=REVERSAL |
| `allocation_order` | int | Order within payment (1..N). Lower = settled earlier per PRD priority |
| `allocation_time` | datetime | When allocation was performed |
| `allocation_rule_version` | varchar(32) | Rule version used by allocation engine (e.g., v1, 2026-01) · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_payment_item_type`:payment_id, statement_item_id, allocation_type (UNIQUE)
- `idx_account_id`:account_id
- `idx_ipa_early_settlement`:early_settlement_id
- `idx_ipa_early_settlement_loan`:early_settlement_loan_id
- `idx_payment_statement`:payment_id, statement_id
- `idx_statement_id`:statement_id
- `idx_statement_item`:statement_item_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
