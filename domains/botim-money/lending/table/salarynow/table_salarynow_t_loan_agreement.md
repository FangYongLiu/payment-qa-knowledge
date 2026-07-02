---
id: tbl_salarynow_t_loan_agreement
object_type: Table
name: Stores signed agreement details for each loan/application under a tenant (t_loan_agreement)
aliases: [t_loan_agreement, salarynow.t_loan_agreement]
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

# Stores signed agreement details for each loan/application under a tenant (t_loan_agreement)

## 用途
物理表 `salarynow.t_loan_agreement`,主键 `id`。Stores signed agreement details for each loan/application under a tenant。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | Primary key: unique identifier for each agreement record · 可空 |
| `member_id` | varchar(32) | Unique identifier of the user/member (same as payby member_id) |
| `application_no` | bigint | Loan or application ID linked to the agreement (numeric long type) |
| `signed_time` | timestamp | Timestamp when the user signed the agreement |
| `agreement_type` | varchar(32) | Type of agreement: KFS, DDA, CREDIT_AGREEMENT, etc. |
| `file_tag` | varchar(128) | Reference name or identifier of the agreement file (e.g., PDF tag or template name) · 可空 |
| `created_time` | timestamp | Record creation time |
| `update_time` | timestamp | Last record update time; updated automatically |

## 主键 / 索引
- 主键:`id`
- `uq_member_application_type`:member_id, application_no, agreement_type (UNIQUE)
- `idx_application_no`:application_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
