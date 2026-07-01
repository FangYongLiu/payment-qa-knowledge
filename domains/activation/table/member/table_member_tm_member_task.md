---
id: tbl_member_tm_member_task
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
- tm_member_task
subdomain: job
module: null
sensitivity: normal
name: job task table(tm_member_task)
aliases:
- tm_member_task
related_services:
- svc_member
related_scenarios: []
---

# job task table(tm_member_task)

## 用途
job task table。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int(10) | PK | Primary Key ID |
| `schedule_id` | int(10) |  | Schedule Id |
| `mode` | varchar(25) | NOT NULL | Process Mode |
| `job_code` | varchar(75) | NOT NULL | Job Code |
| `offset` | int(10) | NOT NULL | Offset |
| `status` | varchar(15) | NOT NULL | INIT, PENDING, FINISH, EXCEPTION |
| `create_time` | timestamp | NOT NULL | Create Time |
| `update_time` | timestamp | NOT NULL | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
