---
id: tbl_sme_t_profile_snap
object_type: Table
name: A snapshot of the user information for the loan order (t_profile_snap)
aliases: [t_profile_snap, sme.t_profile_snap]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# A snapshot of the user information for the loan order (t_profile_snap)

## 用途
物理表 `sme.t_profile_snap`,主键 `id`。A snapshot of the user information for the loan order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `third_user_id` | varchar(20) | Third-party channel user id |
| `third_party_name` | varchar(20) | Order source channel name |
| `mobile` | varchar(32) | Mobile phone number |
| `sex` | tinyint | Surname: 1: female, 2: male · 可空 |
| `birthday` | varchar(10) | birthday · 可空 |
| `name` | varchar(200) | name · 可空 |
| `identity` | varchar(50) | Identification card · 可空 |
| `identity_invalid_time` | varchar(10) | expiration time · 可空 |
| `passport_no` | varchar(50) | Passport number · 可空 |
| `nationality` | varchar(64) | nationality · 可空 |
| `email_address` | varchar(255) | email · 可空 |
| `create_time` | timestamp | Creation time · 可空 |
| `credit_limit` | decimal(15, 4) | Line of credit · 可空 |
| `currency` | char(3) | Monetary unit · 可空 |
| `credit_success_time` | timestamp | Time to obtain credit · 可空 |
| `credit_invalid_time` | timestamp | The expiration or lapse time of the credit · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_id`:loan_order_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
