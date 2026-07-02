---
id: tbl_bps_t_failure_event
object_type: Table
name: log table to record failed events (t_failure_event)
aliases: [t_failure_event, bps.t_failure_event]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# log table to record failed events (t_failure_event)

## 用途
物理表 `bps.t_failure_event`,主键 `id`。log table to record failed events。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 待补 |
| `error_type` | varchar(32) | Error type of the log. eg: SystemError, BusinessError |
| `process_name` | varchar(50) | The name of the process where the error occurred. |
| `error_timestamp` | timestamp | Timestamp when the error occurred. · 可空 |
| `details` | varchar(500) | Details of the error · 可空 |
| `related_entity_id` | char(32) | ID related to the business entity · 可空 |
| `severity_level` | varchar(16) | Error severity. eg: High, Medium, Low · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
