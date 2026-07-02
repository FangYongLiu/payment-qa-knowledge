---
id: tbl_loyalty_t_events_audit_ext_2026_11
object_type: Table
name: Extension table for events audit payload data - 2026-11 (t_events_audit_ext_2026_11)
aliases: [t_events_audit_ext_2026_11, loyalty.t_events_audit_ext_2026_11]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: loyalty schema DDL
tags: [marketing, loyalty]
sensitivity: normal
related_services: []
---

# Extension table for events audit payload data - 2026-11 (t_events_audit_ext_2026_11)

## 用途
物理表 `loyalty.t_events_audit_ext_2026_11`,主键 `id`。Extension table for events audit payload data - 2026-11。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `event_id` | varchar(100) | FK to t_events_audit.event_id |
| `payload` | varchar(2000) | Original event payload (JSON string) · 可空 |
| `talon_response` | varchar(3000) | Full Talon.One API response JSON · 可空 |
| `created_at` | timestamp | Record creation timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_events_audit_ext_event_id`:event_id (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
