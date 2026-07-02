---
id: tbl_loyalty_t_batch_gold_jobs
object_type: Table
name: Batch gold/silver reward upload jobs (t_batch_gold_jobs)
aliases: [t_batch_gold_jobs, loyalty.t_batch_gold_jobs]
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

# Batch gold/silver reward upload jobs (t_batch_gold_jobs)

## 用途
物理表 `loyalty.t_batch_gold_jobs`,主键 `id`。Batch gold/silver reward upload jobs。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key · 可空 |
| `job_id` | varchar(36) | UUID identifier |
| `job_name` | varchar(200) | Admin-supplied unique name used as cross-job dedup key. NULLABLE so the column can be added to pre-existing tables without backfill; new rows must supply a value (enforced by handler). · 可空 |
| `uploaded_by` | varchar(100) | Admin username from SSO session · 可空 |
| `total_records` | int unsigned | Total records in CSV |
| `processed_count` | int unsigned | Records processed so far |
| `success_count` | int unsigned | Records that succeeded |
| `pending_count` | int unsigned | Records waiting on Gold Service (KYC/retry) |
| `failed_count` | int unsigned | Records that failed |
| `total_gold_aed` | decimal(15, 2) | Sum of gold amounts denominated in AED |
| `total_gold_grams` | decimal(18, 8) | Sum of gold amounts denominated in grams |
| `total_silver_aed` | decimal(15, 2) | Sum of silver amounts denominated in AED |
| `total_silver_grams` | decimal(18, 8) | Sum of silver amounts denominated in grams |
| `order_description` | varchar(100) | User-visible description / memo |
| `status` | varchar(20) | pending_review|processing|completed|cancelled |
| `error_message` | varchar(500) | Job-level error if failed · 可空 |
| `started_at` | timestamp | When processing started · 可空 |
| `completed_at` | timestamp | When processing completed · 可空 |
| `created_at` | timestamp | Job creation time |
| `updated_at` | timestamp | Last update time |

## 主键 / 索引
- 主键:`id`
- `uk_batch_gold_job_id`:job_id (UNIQUE)
- `uk_batch_gold_job_name`:job_name (UNIQUE)
- `idx_batch_gold_status`:status, created_at

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
