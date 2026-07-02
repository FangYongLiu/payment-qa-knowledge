---
id: tbl_member_tr_notify_record
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
- tr_notify_record
subdomain: notify
module: null
sensitivity: normal
name: Notify record(tr_notify_record)
aliases:
- tr_notify_record
related_services:
- svc_member
related_scenarios: []
---

# Notify record(tr_notify_record)

## 用途
Notify record。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `record_id` | bigint | PK / NOT NULL | Record id |
| `event_id` | bigint |  | Event id |
| `config_id` | int |  | Config id |
| `biz_type` | varchar(55) |  | Business type |
| `member_id` | varchar(20) | NOT NULL | Member id |
| `target` | varchar(50) |  | Target |
| `method` | varchar(10) |  | Notify method;SMS,MAIL |
| `subject` | varchar(50) |  | Notify subject |
| `template_id` | varchar(50) |  | Notify content |
| `retry_rules` | varchar(50) |  | Retry rules |
| `next_retry_time` | timestamp |  | Next retry time |
| `retry_times` | int | 默认 0 | Retry times |
| `status` | varchar(10) | NOT NULL / 默认 'PROCESS' | Status;PROCESS,FINISH,ERROR,FAIL |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`record_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
