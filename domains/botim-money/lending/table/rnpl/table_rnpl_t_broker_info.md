---
id: tbl_rnpl_t_broker_info
object_type: Table
name: Collaborator Information Table, including landlords, agents (t_broker_info)
aliases: [t_broker_info, rnpl.t_broker_info]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Collaborator Information Table, including landlords, agents (t_broker_info)

## 用途
物理表 `rnpl.t_broker_info`,主键 `id`。Collaborator Information Table, including landlords, agents。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `phone` | varchar(32) | mobile number |
| `name` | varchar(255) | full name · 可空 |
| `display_name` | varchar(255) | name to display in RNPL application (Profile icon) · 可空 |
| `address` | varchar(255) | address · 可空 |
| `company_name` | varchar(128) | intermediary-specific, identifying the company in which the intermediary is located · 可空 |
| `employee_id` | varchar(128) | agency-specific, identifying agency employee ID · 可空 |
| `onboarding_date` | timestamp | intermediary-specific, identifying the date of the intermediary involvement with the employing company · 可空 |
| `create_time` | timestamp | 待补 |
| `status` | smallint | 1: active; -1：inactive |
| `inactivate_date` | timestamp | inactivate time · 可空 |
| `inactivate_reason` | varchar(255) | inactivate reason · 可空 |
| `is_admin` | smallint | is admin:1:yes; -1:false · 可空 |
| `user_id` | varchar(20) | broker_id |
| `email` | varchar(64) | email |
| `pmc_id` | int | Linked PMC ID · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_phone`:phone (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
