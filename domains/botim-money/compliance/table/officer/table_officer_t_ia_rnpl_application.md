---
id: tbl_officer_t_ia_rnpl_application
object_type: Table
name: t_ia_rnpl_application (t_ia_rnpl_application)
aliases: [t_ia_rnpl_application, officer.t_ia_rnpl_application]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: officer schema DDL
tags: [compliance, officer]
sensitivity: normal
related_services: []
---

# t_ia_rnpl_application (t_ia_rnpl_application)

## 用途
物理表 `officer.t_ia_rnpl_application`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `create_by` | varchar(100) | creator · 可空 |
| `create_time` | timestamp | Creation time · 可空 |
| `update_by` | varchar(100) | Updater · 可空 |
| `update_time` | timestamp | Update time · 可空 |
| `version_id` | smallint | Version optimistic lock · 可空 |
| `application_id` | varchar(64) | 进件id |
| `task_name` | varchar(50) | Audit task name · 可空 |
| `member_id` | varchar(20) | user id |
| `phone` | varchar(32) | The users mobile phone number when submitting the application |
| `param_detail` | varchar(255) | List display details |
| `status` | tinyint | Audit result: -1 failed 0 auditing 1 successful |
| `audit_user_uid` | varchar(50) | Auditor id · 可空 |
| `audit_result` | tinyint | Audit status: 0 Initial 1 Completed · 可空 |
| `audit_detail` | varchar(500) | json detail · 可空 |
| `refuse_message` | varchar(255) | Rejection reason · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
