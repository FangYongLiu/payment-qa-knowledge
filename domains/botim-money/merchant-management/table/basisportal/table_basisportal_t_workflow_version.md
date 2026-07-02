---
id: tbl_basisportal_t_workflow_version
object_type: Table
name: workflow version control (t_workflow_version)
aliases: [t_workflow_version, basisportal.t_workflow_version]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# workflow version control (t_workflow_version)

## 用途
物理表 `basisportal.t_workflow_version`,主键 `id`。workflow version control。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `workflow_id` | bigint(21) | workflow definition id |
| `version` | varchar(16) | version |
| `data_form` | varchar(128) | the url of business data form · 可空 |
| `snapshot` | varchar(128) | ufs url of workflow diagram · 可空 |
| `active` | tinyint(1) | 0-no 1-yes · 可空 |
| `saved` | tinyint(1) | 1- saved 0-unsave · 可空 |
| `create_by` | varchar(45) | create user account · 可空 |
| `create_time` | timestamp | create time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
