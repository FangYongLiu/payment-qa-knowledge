---
id: tbl_salarynow_t_loan_reference
object_type: Table
name: References for each loan application (t_loan_reference)
aliases: [t_loan_reference, salarynow.t_loan_reference]
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

# References for each loan application (t_loan_reference)

## 用途
物理表 `salarynow.t_loan_reference`,主键 `id`。References for each loan application。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `application_id` | int | References loan_application.id |
| `ref_no` | int | first or second reference 1- for first and 2- for second |
| `member_id` | varchar(20) | Reference to user_profile.member_id |
| `ref_name` | varchar(128) | Reference name |
| `ref_email` | varchar(64) | Reference email · 可空 |
| `ref_phone` | varchar(32) | Reference phone · 可空 |
| `ref_relation` | varchar(64) | Relationship to applicant · 可空 |
| `ref_validated` | varchar(20) | Whether this reference is validated DONE, "", FAILED, PENDING · 可空 |
| `ref_validation_date` | timestamp | When validation was done · 可空 |
| `created_at` | timestamp | Record creation time |
| `updated_at` | timestamp | Last update time |

## 主键 / 索引
- 主键:`id`
- `uq_loan_reference_application_id_ref_no`:application_id, ref_no (UNIQUE)
- `idx_loan_reference_member_id`:member_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
