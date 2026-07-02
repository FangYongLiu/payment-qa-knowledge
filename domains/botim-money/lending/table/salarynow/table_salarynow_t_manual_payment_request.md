---
id: tbl_salarynow_t_manual_payment_request
object_type: Table
name: Manual payment requests for loan payments processed outside automated system (t_manual_payment_request)
aliases: [t_manual_payment_request, salarynow.t_manual_payment_request]
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

# Manual payment requests for loan payments processed outside automated system (t_manual_payment_request)

## 用途
物理表 `salarynow.t_manual_payment_request`,主键 `id`。Manual payment requests for loan payments processed outside automated system。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `voucher_no` | varchar(100) | Payment voucher number for reference · 可空 |
| `member_id` | varchar(20) | Member identifier - Reference to user_profile.member_id |
| `loan_id` | bigint | Reference to t_loan.id |
| `amount` | decimal(10, 2) | Payment amount requested |
| `status` | varchar(32) | Request status: PENDING, PROCESSING, COMPLETED, REJECTED, CANCELLED |
| `payment_channel` | varchar(50) | Payment channel used: CASH, CHEQUE, BANK_TRANSFER, ONLINE, OTHER · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_manual_payment_loan_id`:loan_id
- `idx_manual_payment_member_id`:member_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
