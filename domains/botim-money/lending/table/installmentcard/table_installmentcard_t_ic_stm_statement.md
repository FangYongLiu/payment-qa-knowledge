---
id: tbl_installmentcard_t_ic_stm_statement
object_type: Table
name: Statement header: one per account per billing cycle (t_ic_stm_statement)
aliases: [t_ic_stm_statement, installmentcard.t_ic_stm_statement]
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

# Statement header: one per account per billing cycle (t_ic_stm_statement)

## 用途
物理表 `installmentcard.t_ic_stm_statement`,主键 `id`。Statement header: one per account per billing cycle。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key (internal statement identifier) · 可空 |
| `account_id` | bigint | Account identifier (logical ref to t_ic_am_account.id, no FK) |
| `statement_no` | varchar(50) | Unique statement number (system-generated, human readable) |
| `cycle_start_date` | date | Start date of billing cycle (inclusive) |
| `cycle_end_date` | date | End date of billing cycle (inclusive) |
| `statement_date` | date | Statement generation date |
| `due_date` | date | Payment due date |
| `currency` | varchar(3) | Statement currency (ISO 4217, e.g., AED) |
| `total_billed_amount` | decimal(18, 2) | Total billed amount (sum of statement items) |
| `minimum_due_amount` | decimal(18, 2) | Minimum amount due for this statement |
| `total_paid_amount` | decimal(18, 2) | Total paid amount applied to this statement |
| `total_outstanding_amount` | decimal(18, 2) | Outstanding = total_billed - total_paid |
| `statement_status` | tinyint | Statement status: 0=CREATED, 1=BILLED, 2=OVERDUE, 3=CLOSED |
| `payment_status` | tinyint | Payment status: 0=UNPAID, 1=PARTIALLY_PAID, 2=PAID |
| `previous_statement_id` | bigint | Previous statement from which balance was carried forward (no FK) · 可空 |
| `late_fee_product_version_id` | bigint | Product version for late fee rules (logical ref to t_ic_pm_product_version.id, no FK) · 可空 |
| `closed_at` | datetime | Timestamp when the statement was fully closed/settled · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_account_cycle`:account_id, cycle_start_date, cycle_end_date (UNIQUE)
- `uk_statement_no`:statement_no (UNIQUE)
- `idx_previous_statement`:previous_statement_id
- `idx_statement_date`:statement_date

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
