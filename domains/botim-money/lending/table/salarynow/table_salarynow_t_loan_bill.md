---
id: tbl_salarynow_t_loan_bill
object_type: Table
name: Simplified loan bills without direct repayment references (t_loan_bill)
aliases: [t_loan_bill, salarynow.t_loan_bill]
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

# Simplified loan bills without direct repayment references (t_loan_bill)

## 用途
物理表 `salarynow.t_loan_bill`,主键 `id`。Simplified loan bills without direct repayment references。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `loan_id` | bigint | Reference to loan.id |
| `member_id` | varchar(20) | Member identifier |
| `amount` | decimal(10, 2) | Bill amount |
| `paid_amount` | decimal(10, 2) | Total amount paid against this bill |
| `status` | varchar(32) | Bill status: PENDING, PARTIAL_PAID, PAID |
| `created_at` | timestamp | Creation timestamp |
| `updated_at` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_bill_loan_id`:loan_id
- `idx_bill_member_id`:member_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
