---
id: tbl_loyalty_t_worker_state
object_type: Table
name: Talon.One synchronization state tracking (t_worker_state)
aliases: [t_worker_state, loyalty.t_worker_state]
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

# Talon.One synchronization state tracking (t_worker_state)

## 用途
物理表 `loyalty.t_worker_state`,主键 `id`。Talon.One synchronization state tracking。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `worker_type` | varchar(50) | Worker identifier (campaigns, bigdata_user_sync, talon_profile_sync, inventory_sync, api_rate_limit, etc.) |
| `application_id` | int | Talon.One application ID (if applicable) · 可空 |
| `last_sync_at` | timestamp | When last successful sync completed · 可空 |
| `last_sync_cursor` | varchar(200) | Cursor/offset for pagination · 可空 |
| `last_sync_etag` | varchar(100) | ETag for change detection · 可空 |
| `last_sync_count` | int unsigned | Number of records synced · 可空 |
| `last_sync_status` | varchar(10) | Last sync status: success|partial|failed · 可空 |
| `last_error` | varchar(100) | Last sync error message · 可空 |
| `next_sync_at` | timestamp | Scheduled next sync time · 可空 |
| `sync_interval_sec` | int unsigned | Sync interval in seconds |
| `is_enabled` | tinyint(1) | Whether sync is enabled |
| `metadata` | varchar(750) | Additional metadata (JSON string) · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |
| `batch_size` | int unsigned | Batch size for sync worker (0 = use config default) |

## 主键 / 索引
- 主键:`id`
- `uk_worker_type`:application_id, worker_type (UNIQUE)
- `idx_worker_next_sync`:next_sync_at, is_enabled

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
