---
id: tbl_member_tr_notify_event
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
- notify
- tr_notify_event
subdomain: notify
module: null
sensitivity: normal
name: Notify event(tr_notify_event)
aliases:
- tr_notify_event
related_services:
- svc_member
related_scenarios: []
---

# Notify event(tr_notify_event)

## 用途
Notify event。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `event_id` | bigint | PK / NOT NULL | Event id |
| `member_id` | varchar(20) | NOT NULL | Member id |
| `config_id` | int |  | Config id |
| `target` | varchar(50) |  | Target |
| `expiry_time` | timestamp |  | Expiry Time |
| `next_time` | timestamp |  | Next notify time |
| `finish_time` | timestamp |  | Finish Time |
| `notify_rules` | varchar(50) |  | Notify rules |
| `notify_times` | int | 默认 0 | Notify times |
| `event_type` | varchar(25) |  | Event Type |
| `status` | varchar(10) | NOT NULL / 默认 'PROCESS' | Status;PROCESS,FINISH,INVALID |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`event_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
