---
id: tbl_salarynow_t_application_loan_repayment_snapshot
object_type: Table
name: Per-installment repayment snapshot for a loan pricing snapshot (t_application_loan_repayment_snapshot)
aliases: [t_application_loan_repayment_snapshot, salarynow.t_application_loan_repayment_snapshot]
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

# Per-installment repayment snapshot for a loan pricing snapshot (t_application_loan_repayment_snapshot)

## 用途
物理表 `salarynow.t_application_loan_repayment_snapshot`,主键 `id`。Per-installment repayment snapshot for a loan pricing snapshot。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `loan_snapshot_id` | bigint | FK -> t_application_loan_snapshot.id |
| `installment_no` | int | Installment sequence number (1..tenure) |
| `opening_balance` | decimal(10, 2) | Opening balance before this installment |
| `emi_amount` | decimal(10, 2) | EMI for this installment |
| `profit_amount` | decimal(10, 2) | Interest/profit component of EMI |
| `principal` | decimal(10, 2) | Principal component of EMI |
| `closing_balance` | decimal(10, 2) | Balance after this installment |
| `due_date` | date | Due date for this installment |
| `created_at` | timestamp | Row creation time |
| `updated_at` | timestamp | Row last update time |

## 主键 / 索引
- 主键:`id`
- `uq_rep_snapshot_installment`:loan_snapshot_id, installment_no (UNIQUE)
- `idx_rep_snapshot_due_date`:due_date

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
