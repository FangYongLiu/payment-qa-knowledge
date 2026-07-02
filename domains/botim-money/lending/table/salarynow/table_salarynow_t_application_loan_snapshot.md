---
id: tbl_salarynow_t_application_loan_snapshot
object_type: Table
name: Snapshot of computed loan pricing displayed to user (t_application_loan_snapshot)
aliases: [t_application_loan_snapshot, salarynow.t_application_loan_snapshot]
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

# Snapshot of computed loan pricing displayed to user (t_application_loan_snapshot)

## 用途
物理表 `salarynow.t_application_loan_snapshot`,主键 `id`。Snapshot of computed loan pricing displayed to user。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(20) | Member identifier (string) |
| `application_id` | bigint | Related application id |
| `product_id` | bigint | Related product id |
| `irr` | decimal(10, 2) | Internal rate of return (%) |
| `interest_rate_percentage` | decimal(10, 2) | Interest rate percentage for the loan |
| `processing_fee` | decimal(10, 2) | Processing fee amount |
| `processing_fee_vat_amount` | decimal(12, 2) | Processing fee VAT amount · 可空 |
| `processing_fee_vat_percentage` | decimal(10, 2) | Processing fee VAT percentage · 可空 |
| `total_interest` | decimal(10, 2) | Total interest over the tenure |
| `disburse_amount` | decimal(10, 2) | Net disbursed amount |
| `disburse_account` | varchar(64) | Account to disburse to · 可空 |
| `repay_account` | varchar(64) | Account to collect repayments from · 可空 |
| `first_due_date` | date | First scheduled due date |
| `last_due_date` | date | Last scheduled due date |
| `created_at` | timestamp | Row creation time |
| `updated_at` | timestamp | Row last update time |

## 主键 / 索引
- 主键:`id`
- `idx_snapshot_application_id`:application_id
- `idx_snapshot_member_id`:member_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
