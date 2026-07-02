---
id: tbl_loyalty_t_cache_warming_jobs
object_type: Table
name: Tracks L4 cache warming jobs for user audience membership. Created during campaign sync when audiences change. (t_cache_warming_jobs)
aliases: [t_cache_warming_jobs, loyalty.t_cache_warming_jobs]
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

# Tracks L4 cache warming jobs for user audience membership. Created during campaign sync when audiences change. (t_cache_warming_jobs)

## 用途
物理表 `loyalty.t_cache_warming_jobs`,主键 `id`。Tracks L4 cache warming jobs for user audience membership. Created during campaign sync when audiences change.。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `job_type` | varchar(30) | Job type: audience|user_profile|user_achievement |
| `audience_id` | bigint unsigned | Internal audience ID (only for audience jobs) · 可空 |
| `talon_audience_id` | int | Talon.One audience ID (only for audience jobs) · 可空 |
| `campaign_id` | bigint unsigned | Campaign that triggered this warming (NULL for manual warming) · 可空 |
| `member_count` | int unsigned | Total members in audience (from t_audiences.member_count) |
| `warmed_count` | int unsigned | Members processed so far (for progress tracking) |
| `pk_range_start` | bigint unsigned | PK range start (exclusive) for user_profile jobs; batch offset for legacy user_achievement jobs |
| `pk_range_end` | bigint unsigned | PK range end (inclusive) for user_profile jobs; batch limit for legacy user_achievement jobs |
| `total_count` | int unsigned | Total items to warm (for progress display) |
| `status` | varchar(15) | Job status: pending|processing|completed|failed|cancelled |
| `triggered_by` | varchar(50) | What triggered this job: campaign_sync|manual|api · 可空 |
| `error_message` | varchar(500) | Error message if failed · 可空 |
| `retry_count` | int unsigned | Number of retry attempts |
| `started_at` | timestamp | When processing started · 可空 |
| `completed_at` | timestamp | When processing completed · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_warming_audience`:audience_id
- `idx_warming_campaign`:campaign_id
- `idx_warming_job_type`:job_type, status
- `idx_warming_status`:status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
