---
id: tbl_salarynow_t_pay_settlement_log
object_type: Table
name: Payment settlement log - tracks how payments are allocated to specific bill items (t_pay_settlement_log)
aliases: [t_pay_settlement_log, salarynow.t_pay_settlement_log]
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

# Payment settlement log - tracks how payments are allocated to specific bill items (t_pay_settlement_log)

## 用途
物理表 `salarynow.t_pay_settlement_log`,主键 `id`。Payment settlement log - tracks how payments are allocated to specific bill items。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(20) | Member identifier - Reference to user_profile.member_id |
| `loan_id` | bigint | Reference to t_loan.id |
| `payment_id` | bigint | Reference to t_loan_payment.id |
| `bill_id` | bigint | Reference to t_loan_bill.id |
| `bill_item_id` | bigint | Reference to t_bill_item.id |
| `amount` | decimal(10, 2) | Settlement amount |
| `created_at` | timestamp | Creation timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_pay_settlement_loan_id`:loan_id
- `idx_pay_settlement_member_id`:member_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
