---
id: tbl_collection_t_ia_rnpl_application
object_type: Table
name: rnpl_application (t_ia_rnpl_application)
aliases: [t_ia_rnpl_application, collection.t_ia_rnpl_application]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# rnpl_application (t_ia_rnpl_application)

## 用途
物理表 `collection.t_ia_rnpl_application`,主键 `id`。rnpl_application。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `create_by` | varchar(64) | create_by · 可空 |
| `create_time` | timestamp | create_time · 可空 |
| `update_by` | varchar(64) | update_by · 可空 |
| `update_time` | timestamp | update_time · 可空 |
| `version_id` | smallint(5) | version_id · 可空 |
| `application_id` | varchar(64) | application_id |
| `task_name` | varchar(50) | task_name · 可空 |
| `member_id` | varchar(20) | user_id |
| `phone` | varchar(32) | mobile phone |
| `param_detail` | varchar(255) | show detail |
| `status` | tinyint(3) | status: -1=fail 0=init 1=success |
| `audit_user_uid` | varchar(50) | audit_user_uid · 可空 |
| `audit_result` | tinyint(3) | audit staut: 0=init 1=finish  · 可空 |
| `audit_detail` | varchar(500) | json detail · 可空 |
| `refuse_message` | varchar(255) | refuse_message · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_application_id`:application_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
