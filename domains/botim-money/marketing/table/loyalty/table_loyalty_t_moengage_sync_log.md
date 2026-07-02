---
id: tbl_loyalty_t_moengage_sync_log
object_type: Table
name: MoEngage webhook audit trail and idempotency tracking (t_moengage_sync_log)
aliases: [t_moengage_sync_log, loyalty.t_moengage_sync_log]
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

# MoEngage webhook audit trail and idempotency tracking (t_moengage_sync_log)

## 用途
物理表 `loyalty.t_moengage_sync_log`,主键 `id`。MoEngage webhook audit trail and idempotency tracking。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Auto-increment primary key · 可空 |
| `moengage_sync_id` | varchar(50) | MoEngage segment/sync identifier (maps to t_audiences.source_cohort_id) |
| `moengage_sync_name` | varchar(50) | Human-readable segment name from MoEngage |
| `moengage_execution_id` | varchar(50) | Unique identifier for this execution (for idempotency) |
| `moengage_integration_id` | varchar(50) | MoEngage integration configuration ID · 可空 |
| `page_count` | int unsigned | Current page number (1-indexed) |
| `talon_audience_id` | int | Talon.One audience ID (from t_audiences.talon_audience_id) · 可空 |
| `users_added` | int unsigned | Successfully added to Talon.One and database |
| `users_removed` | int unsigned | Successfully removed from Talon.One and database |
| `users_failed` | int unsigned | Failed to process (Talon API error or invalid ID) |
| `status` | varchar(20) | processing | success | partial | failed |
| `error_message` | varchar(500) | Error details if status=failed or partial · 可空 |
| `duration_ms` | int unsigned | Time taken to process webhook (milliseconds) · 可空 |
| `created_at` | timestamp | Webhook received timestamp · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_execution_id_page`:moengage_execution_id, page_count (UNIQUE)
- `idx_created_at`:created_at
- `idx_sync_id`:moengage_sync_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
