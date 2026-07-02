---
id: tbl_atbeb_t_event
object_type: Table
name: events to be retried (t_event)
aliases: [t_event, atbeb.t_event]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: atbeb schema DDL
tags: [marketing, atbeb]
sensitivity: normal
related_services: []
---

# events to be retried (t_event)

## 用途
物理表 `atbeb.t_event`,主键 `id`。events to be retried。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Auto-incrementing primary key · 可空 |
| `event_id` | varchar(80) | event id |
| `event_type` | varchar(50) | event type |
| `content` | varchar(2048) | event content · 可空 |
| `status` | tinyint | Status, 0-waiting, 1-success, 2-failed |
| `create_at` | datetime | Create timestamp |
| `update_at` | datetime | Update timestamp |

## 主键 / 索引
- 主键:`id`
- `uniq_idx_event_id`:event_id (UNIQUE)
- `idx_status`:status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
