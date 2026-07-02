---
id: tbl_salarynow_t_loan_application
object_type: Table
name: Loan applications with application number and audit fields (t_loan_application)
aliases: [t_loan_application, salarynow.t_loan_application]
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

# Loan applications with application number and audit fields (t_loan_application)

## 用途
物理表 `salarynow.t_loan_application`,主键 `id`。Loan applications with application number and audit fields。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `application_no` | varchar(64) | Application number from offer · 可空 |
| `member_id` | varchar(20) | Reference to user_profile.member_id |
| `offer_id` | varchar(32) | Reference to loan_offer.offer_no |
| `email` | varchar(64) | Applicant email · 可空 |
| `alt_phone` | varchar(32) | alternate phone · 可空 |
| `status` | varchar(32) | Application status: CREATED, VERIFICATION, APPROVED, REJECTED, ACCEPTED, REJECTED_BY_USER, EXPIRED |
| `selected_tenure` | int | Selected tenure in months · 可空 |
| `selected_amount` | decimal(10, 2) | Selected loan amount · 可空 |
| `calculation_date` | timestamp | Date when calculation was done · 可空 |
| `expiry_date` | timestamp | Expiry date for the application · 可空 |
| `otp_verification` | varchar(20) | Whether OTP verification is DONE, PENDING, FAILED |
| `face_verification` | varchar(20) | Whether FACE verification is DONE, PENDING, FAILED |
| `verification_date` | timestamp | OTP verification date · 可空 |
| `created_at` | timestamp | Application creation time |
| `updated_at` | timestamp | Last update time |
| `risk_decision_timestamp` | timestamp | Timestamp when risk decision was made (APPROVED/REJECTED) · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_loan_application_application_no`:application_no
- `idx_loan_application_member_id`:member_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
