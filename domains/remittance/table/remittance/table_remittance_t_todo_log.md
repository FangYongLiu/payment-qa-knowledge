---
id: tbl_remittance_t_todo_log
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_todo_log
subdomain: remittance
module: null
sensitivity: normal
name: To-Do Log Table(t_todo_log)
aliases:
- t_todo_log
related_services:
- svc_remittance
related_scenarios: []
---
# To-Do Log Table(t_todo_log)

## 用途
To-Do Log Table。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key ID |
| `member_id` | varchar(20) | NOT NULL | Member ID |
| `uid` | varchar(32) | NOT NULL | Unique BOTIM identifier |
| `status` | tinyint | NOT NULL / 默认 0 | Status: 0-Created, 1-Completed |
| `scenario` | varchar(32) | NOT NULL | Business Scenario |
| `create_time` | timestamp | NOT NULL | Creation Time |
| `update_time` | timestamp | NOT NULL | Last Update Time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_uid_sce` 唯一 (uid, scenario)
- 索引:
  - `idx_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
