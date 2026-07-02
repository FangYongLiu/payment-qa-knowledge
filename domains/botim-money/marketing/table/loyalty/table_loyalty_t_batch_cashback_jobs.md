---
id: tbl_loyalty_t_batch_cashback_jobs
object_type: Table
name: Batch cashback upload jobs (t_batch_cashback_jobs)
aliases: [t_batch_cashback_jobs, loyalty.t_batch_cashback_jobs]
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

# Batch cashback upload jobs (t_batch_cashback_jobs)

## 用途
物理表 `loyalty.t_batch_cashback_jobs`,主键 `id`。Batch cashback upload jobs。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key · 可空 |
| `job_id` | varchar(36) | UUID identifier |
| `job_name` | varchar(200) | Admin-supplied unique name; new uploads must populate this. NULL only on legacy rows that predate this migration. · 可空 |
| `uploaded_by` | varchar(100) | Admin username from SSO session · 可空 |
| `total_records` | int unsigned | Total records in CSV |
| `processed_count` | int unsigned | Records processed so far |
| `success_count` | int unsigned | Records that succeeded |
| `pending_count` | int unsigned | Records where M2U accepted but body status is non-terminal (e.g. WAITING) |
| `failed_count` | int unsigned | Records that failed |
| `total_amount_requested` | decimal(15, 2) | Sum of amounts in CSV |
| `total_amount_credited` | decimal(15, 2) | Sum of amounts actually credited |
| `currency` | varchar(3) | Currency for all transfers |
| `order_description` | varchar(100) | User-visible description in PayBy app |
| `status` | varchar(20) | pending_review|processing|completed|cancelled |
| `error_message` | varchar(500) | Job-level error if failed · 可空 |
| `started_at` | timestamp | When processing started · 可空 |
| `completed_at` | timestamp | When processing completed · 可空 |
| `created_at` | timestamp | 待补 |
| `updated_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_batch_cashback_job_id`:job_id (UNIQUE)
- `uk_batch_cashback_job_name`:job_name (UNIQUE)
- `idx_batch_cashback_status`:status, created_at

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
