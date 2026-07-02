---
id: tbl_loyalty_t_events_audit_2026_01
object_type: Table
name: Audit log of all processed events from at-beb - 2026-01 (t_events_audit_2026_01)
aliases: [t_events_audit_2026_01, loyalty.t_events_audit_2026_01]
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

# Audit log of all processed events from at-beb - 2026-01 (t_events_audit_2026_01)

## 用途
物理表 `loyalty.t_events_audit_2026_01`,主键 `id`。Audit log of all processed events from at-beb - 2026-01。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `event_id` | varchar(100) | Unique event ID for idempotency (from at-beb) |
| `event_type` | varchar(100) | Event type from at-beb: payby.biz.internation_transtfer, payby.biz.kyc, botim.ai, botim.ogold |
| `event_name` | varchar(200) | Event name from at-beb: International Transfer Successful, etc. |
| `event_time` | bigint unsigned | Event timestamp from at-beb (Unix ms) · 可空 |
| `ucid` | varchar(50) | User UCID who triggered the event |
| `producer` | varchar(100) | Service that produced the event (e.g., payby) · 可空 |
| `status` | varchar(20) | Processing status: received|processing|processed|failed|skipped|duplicate|retrying|permanently_failed |
| `error_message` | varchar(100) | Error message if failed · 可空 |
| `error_code` | varchar(50) | Error code: transformation_error, talon_api_error, effects_processing_error · 可空 |
| `talon_session_id` | varchar(100) | Talon.One session ID created for this event · 可空 |
| `talon_effects_count` | int unsigned | Number of effects returned by Talon.One |
| `processing_started_at` | timestamp | When processing started · 可空 |
| `processing_duration_ms` | int unsigned | Processing duration in milliseconds · 可空 |
| `processed_at` | timestamp | When processing completed · 可空 |
| `retry_count` | int unsigned | Number of retry attempts |
| `max_retries` | int unsigned | Maximum retry attempts |
| `next_retry_at` | timestamp | When next retry should be attempted · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_events_audit_event_id`:event_id (UNIQUE)
- `idx_events_audit_retry`:next_retry_at, status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
