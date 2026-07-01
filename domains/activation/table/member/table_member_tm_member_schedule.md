---
id: tbl_member_tm_member_schedule
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- job
- tm_member_schedule
subdomain: job
module: null
sensitivity: normal
name: job schedule table(tm_member_schedule)
aliases:
- tm_member_schedule
related_services:
- svc_member
related_scenarios: []
---

# job schedule table(tm_member_schedule)

## 用途
job schedule table。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK | Primary Key ID |
| `job_name` | varchar(75) | NOT NULL | Job Name |
| `job_code` | varchar(75) | NOT NULL | Job Code |
| `mode` | varchar(25) | NOT NULL | Process Mode: PAGE,RANGE,DATE,DTIME |
| `offset` | int(10) | NOT NULL | Offset |
| `cron` | varchar(22) |  | Expression |
| `last_trigger_time` | timestamp |  | Last Trigger Time |
| `next_trigger_time` | timestamp |  | Next Trigger Time |
| `enable` | char | NOT NULL | Is enable, Y/N |
| `create_time` | timestamp | NOT NULL | Create Time |
| `update_time` | timestamp | NOT NULL | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
