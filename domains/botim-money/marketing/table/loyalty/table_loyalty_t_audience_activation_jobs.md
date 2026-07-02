---
id: tbl_loyalty_t_audience_activation_jobs
object_type: Table
name: t_audience_activation_jobs (t_audience_activation_jobs)
aliases: [t_audience_activation_jobs, loyalty.t_audience_activation_jobs]
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

# t_audience_activation_jobs (t_audience_activation_jobs)

## 用途
物理表 `loyalty.t_audience_activation_jobs`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `audience_id` | bigint unsigned | Internal audience ID (t_audiences.id) |
| `talon_audience_id` | int | Talon.One audience ID (for API call + logging) |
| `campaign_id` | bigint unsigned | Internal campaign ID (t_campaigns.id) — the follow-up campaign wired to audience_id |
| `user_filter_kind` | varchar(20) | list (explicit integration_ids) | all_members (stream every member of audience_id) |
| `user_filter` | text | JSON-encoded array of integration_ids when user_filter_kind=list; NULL when all_members. Producers cap each row at 700 ids (~51 KB serialized) so it stays well under TEXTs 64 KB cap; large inputs are split across multiple rows via batch_id/batch_seq. · 可空 |
| `triggered_by` | varchar(50) | Source of the job: moengage_sync | csv_upload | campaign_sync |
| `batch_id` | varchar(36) | UUID per producer call. All chunks of one CSV upload (or MoEngage page) share this id so chunks of the same batch can be rolled up in the dashboard. |
| `batch_seq` | int unsigned | Chunk index within the batch, 0..N-1. Always 0 for batches that fit in a single chunk (MoEngage pages, campaign-sync backfill rows). |
| `total_count` | int unsigned | Total users to process in this chunk (known up-front for list jobs; populated at processing time for all_members) · 可空 |
| `processed_count` | int unsigned | Users processed so far (activated + skipped + failed) |
| `activated_count` | int unsigned | Users where the rule fired and a t_user_achievements row was written |
| `skipped_count` | int unsigned | Users skipped via bitmap + DB pre-check (already activated) |
| `failed_count` | int unsigned | Users where the API call or upsert failed |
| `status` | varchar(15) | Job status: ready | processing | completed | failed | cancelled |
| `error_message` | varchar(500) | Error message if status=failed · 可空 |
| `retry_count` | int unsigned | Number of retry attempts (incremented when stuck-job recovery resets to ready) |
| `started_at` | timestamp | When processing started (used by stuck-job recovery: started_at < NOW() - timeout → reset to ready) · 可空 |
| `completed_at` | timestamp | When processing completed or failed · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_activation_chunk`:audience_id, campaign_id, batch_id, batch_seq (UNIQUE)
- `idx_activation_created`:created_at
- `idx_status_created_at`:status, created_at

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
