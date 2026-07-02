---
id: tbl_salarynow_t_fee_and_fine
object_type: Table
name: Fee and fine management for loans and repayments (t_fee_and_fine)
aliases: [t_fee_and_fine, salarynow.t_fee_and_fine]
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

# Fee and fine management for loans and repayments (t_fee_and_fine)

## 用途
物理表 `salarynow.t_fee_and_fine`,主键 `id`。Fee and fine management for loans and repayments。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `type` | varchar(32) | Fee/fine type: PROCESSING_FEE, LATE_FEE, PENALTY_FEE, VAT, OTHER |
| `member_id` | varchar(20) | Member identifier - Reference to user_profile.member_id |
| `loan_id` | bigint | Reference to t_loan.id |
| `repayment_id` | bigint | Reference to t_loan_repayment.id (nullable for loan-level fees) · 可空 |
| `amount` | decimal(10, 2) | Fee/fine amount |
| `vat_amount` | decimal(10, 2) | VAT amount calculated for this fee/fine · 可空 |
| `vat_percentage` | decimal(10, 2) | VAT percentage used for calculation · 可空 |
| `description` | varchar(255) | Description of the fee/fine · 可空 |
| `pay_status` | varchar(20) | Payment status: UNPAID, PARTIAL_PAID, PAID |
| `paid_at` | timestamp | Timestamp when fully paid · 可空 |
| `created_at` | timestamp | Creation timestamp |
| `updated_at` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_fee_fine_loan_id`:loan_id
- `idx_fee_fine_member_id`:member_id
- `idx_fee_fine_repayment_id`:repayment_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
