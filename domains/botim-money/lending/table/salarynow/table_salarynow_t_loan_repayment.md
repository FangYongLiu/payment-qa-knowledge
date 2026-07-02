---
id: tbl_salarynow_t_loan_repayment
object_type: Table
name: Repayment for a loan (t_loan_repayment)
aliases: [t_loan_repayment, salarynow.t_loan_repayment]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: salarynow schema DDL
tags: [lending, salarynow]
sensitivity: normal
related_services: []
---

# Repayment for a loan (t_loan_repayment)

## 用途
物理表 `salarynow.t_loan_repayment`,主键 `id`。Repayment for a loan。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `loan_id` | bigint | t_loan.id |
| `product_id` | bigint | Reference to t_product.id |
| `installment_no` | int | Installment sequence number (1..tenure) |
| `opening_balance` | decimal(10, 2) | Opening balance before this installment |
| `emi_amount` | decimal(10, 2) | EMI for this installment |
| `profit_amount` | decimal(10, 2) | Interest/profit component of EMI |
| `principal` | decimal(10, 2) | Principal component of EMI |
| `closing_balance` | decimal(10, 2) | Balance after this installment |
| `due_date` | date | Due date for this installment |
| `due_month` | varchar(7) | Due month in YYYY-MM format |
| `status` | varchar(20) | SCHEDULED, PARTIAL, PAID, OVERDUE, WRITEOFF |
| `paid_at` | timestamp | Fully payment date · 可空 |
| `updated_at` | timestamp | Row last update time |
| `created_at` | timestamp | Row creation time |

## 主键 / 索引
- 主键:`id`
- `uq_t_loan_repayment_loan_id_installment_no`:loan_id, installment_no (UNIQUE)
- `idx_loan_repayment_due_month`:due_month
- `idx_t_loan_repayment_due_date_product_id`:due_date, product_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
