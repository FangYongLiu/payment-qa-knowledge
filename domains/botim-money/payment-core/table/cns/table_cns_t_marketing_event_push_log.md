---
id: tbl_cns_t_marketing_event_push_log
object_type: Table
name: Marketing event push log table (t_marketing_event_push_log)
aliases: [t_marketing_event_push_log, cns.t_marketing_event_push_log]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cns schema DDL
tags: [payment-core, cns]
sensitivity: normal
related_services: []
---

# Marketing event push log table (t_marketing_event_push_log)

## 用途
物理表 `cns.t_marketing_event_push_log`,主键 `id`。Marketing event push log table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key ID (format: YYYYMMDD + 9-digit seq) |
| `member_id` | varchar(20) | Member ID |
| `event_id` | varchar(64) | Event ID |
| `event_type` | varchar(32) | Event type |
| `event_name` | varchar(128) | Event name |
| `event_time` | timestamp | Event time · 可空 |
| `execute_result` | char | F=Failed, S=SUCCESSFUL · 可空 |
| `error_message` | varchar(255) | Error message · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |
| `push_payload` | varchar(512) | Serialized at-beb payload, for compensation retry · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_event_id`:event_id (UNIQUE)
- `idx_create_time`:create_time
- `idx_event_time`:event_time
- `idx_member_id`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
