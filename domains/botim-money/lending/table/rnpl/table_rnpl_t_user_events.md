---
id: tbl_rnpl_t_user_events
object_type: Table
name: t_user_events (t_user_events)
aliases: [t_user_events, rnpl.t_user_events]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# t_user_events (t_user_events)

## 用途
物理表 `rnpl.t_user_events`,主键 `event_log_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `event_log_id` | int | Unique sequence-generated ID · 可空 |
| `event_name` | varchar(100) | Unique name assigned for the event (e.g., 'pay_button_click') |
| `event_timestamp` | datetime | Timestamp of the event (dd/mm/yyyy hh:mi:ss) |
| `user_id` | varchar(50) | Unique identifier of the user (UUID or ID) |
| `device_info` | varchar(512) | JSON field to store device metadata (OS, Model, App Version) · 可空 |
| `event_data` | varchar(512) | JSON field for additional event details · 可空 |
| `created_at` | timestamp | Auto timestamp for insertion · 可空 |

## 主键 / 索引
- 主键:`event_log_id`
- `idx_user_events_id`:user_id
- `idx_user_events_name`:event_name

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
