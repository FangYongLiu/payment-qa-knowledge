---
id: tbl_statementii_t_retry_task
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (statementii schema) 2026-06-25
tags:
- statementii
- statement
- t_retry_task
subdomain: statement
module: null
sensitivity: normal
name: 重试任务(t_retry_task)
aliases:
- t_retry_task
related_services:
- svc_statementii
related_scenarios: []
---
# 重试任务(t_retry_task)

## 用途
重试任务。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id 主键 |
| `task_id` | bigint | NOT NULL | 任务id |
| `task_status` | varchar(32) | NOT NULL | 任务状态 |
| `retry_times` | int | NOT NULL | 重试次数 |
| `next_exe_time` | timestamp | NOT NULL | 下次执行时间 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uidx_task_id_status` 唯一 (task_id, task_status)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
