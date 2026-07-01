---
id: tbl_remittance_t_channel_notify
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
- t_channel_notify
subdomain: remittance
module: null
sensitivity: normal
name: Channel Notify(t_channel_notify)
aliases:
- t_channel_notify
related_services:
- svc_remittance
related_scenarios: []
---
# Channel Notify(t_channel_notify)

## 用途
Channel Notify。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | id |
| `channel_code` | varchar(32) | NOT NULL | Channel code |
| `notify_type` | varchar(25) | NOT NULL | Event type |
| `notify_content` | varchar(1500) | NOT NULL | Notify content |
| `allow_time` | timestamp | NOT NULL | Allow time |
| `execute_status` | char(3) | NOT NULL | Execute status: I - Initialize ,IGN - Ignore,S - Success,F -Fail |
| `retry_times` | int(4) | NOT NULL / 默认 0 | Retry Times |
| `error_message` | varchar(128) |  | Error message |
| `save_history` | char | NOT NULL | Save history: Y/N |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_allow_time` (allow_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
