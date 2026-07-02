---
id: tbl_installmentcard_t_ic_stm_statement_item
object_type: Table
name: Statement line items: installments, fees, VAT, previous balance (t_ic_stm_statement_item)
aliases: [t_ic_stm_statement_item, installmentcard.t_ic_stm_statement_item]
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

# Statement line items: installments, fees, VAT, previous balance (t_ic_stm_statement_item)

## 用途
物理表 `installmentcard.t_ic_stm_statement_item`,主键 `id`。Statement line items: installments, fees, VAT, previous balance。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `statement_id` | bigint | Logical ref to t_ic_stm_statement.id (no FK) |
| `account_id` | bigint | Account identifier (denormalized for faster queries, no FK) |
| `item_type` | tinyint | Item type: 0=INSTALLMENT_PRINCIPAL, 1=INSTALLMENT_INTEREST, 2=LATE_FEE, 3=LATE_FEE_VAT, 4=OVERLIMIT_FEE, 5=OVERLIMIT_FEE_VAT, 6=PROCESSING_FEE, 7=PROCESSING_FEE_VAT, 8=PREVIOUS_BALANCE |
| `ref_id` | bigint | Reference id (e.g., installment_id for principal/interest). NULL for fees · 可空 |
| `priority_order` | int | Payment allocation priority. Lower = paid first |
| `original_amount` | decimal(18, 2) | Original billed amount |
| `paid_amount` | decimal(18, 2) | Total paid against this item |
| `outstanding_amount` | decimal(18, 2) | Remaining outstanding (initially = original_amount) |
| `currency` | varchar(3) | Currency (ISO 4217, e.g., AED) |
| `item_status` | tinyint | Item status: 0=UNPAID, 1=PARTIALLY_PAID, 2=PAID, 3=WAIVED |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_stmt_item_unique`:statement_id, item_type, ref_id (UNIQUE)
- `idx_account_id`:account_id
- `idx_item_type`:item_type
- `idx_ref_id`:ref_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
