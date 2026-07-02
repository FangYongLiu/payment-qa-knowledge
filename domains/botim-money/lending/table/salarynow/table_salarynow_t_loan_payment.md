---
id: tbl_salarynow_t_loan_payment
object_type: Table
name: Payments made against loan bills (t_loan_payment)
aliases: [t_loan_payment, salarynow.t_loan_payment]
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

# Payments made against loan bills (t_loan_payment)

## 用途
物理表 `salarynow.t_loan_payment`,主键 `id`。Payments made against loan bills。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `bill_id` | bigint | Reference to t_loan_bill.id · 可空 |
| `loan_id` | bigint | Reference to loan.id · 可空 |
| `member_id` | varchar(20) | Member identifier · 可空 |
| `amount` | decimal(10, 2) | Payment amount |
| `settled_amount` | decimal(10, 2) | Amount that has been settled/allocated to bills · 可空 |
| `payment_method` | varchar(32) | Payment method: CAPITAL_RECOVERY, MANUAL |
| `payment_reference` | varchar(64) | External payment reference · 可空 |
| `created_at` | timestamp | Payment timestamp |
| `updated_at` | timestamp | Last update timestamp |
| `pay_request_id` | bigint | Payment request identifier · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_loan_payment_loan_id`:loan_id
- `idx_loan_payment_member_id`:member_id
- `idx_loan_payment_pay_request_id`:pay_request_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
