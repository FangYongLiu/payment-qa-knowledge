---
id: tbl_loyalty_t_budget_removal_jobs
object_type: Table
name: Async job queue for budget-exhaustion-triggered Not-Started-user removal. Mirrors t_audience_activation_jobs worker pattern. (t_budget_removal_jobs)
aliases: [t_budget_removal_jobs, loyalty.t_budget_removal_jobs]
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

# Async job queue for budget-exhaustion-triggered Not-Started-user removal. Mirrors t_audience_activation_jobs worker pattern. (t_budget_removal_jobs)

## 用途
物理表 `loyalty.t_budget_removal_jobs`,主键 `id`。Async job queue for budget-exhaustion-triggered Not-Started-user removal. Mirrors t_audience_activation_jobs worker pattern.。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `campaign_id` | bigint unsigned | Campaign whose budget was exhausted (FK to t_campaigns.id). |
| `status` | varchar(15) | Job status: ready | processing | completed | failed |
| `active_marker` | varchar(8) | 待补 · 可空 |
| `else` | NULL | Virtual column: "active" for in-flight statuses, NULL otherwise. NULL values do not conflict in UNIQUE, so multiple historical completed/failed rows can coexist per campaign, while at most one active row is enforced. · 可空 |
| `processed_count` | int unsigned | Audience members visited (activated + skipped + failed). |
| `inserted_count` | int unsigned | Rows inserted with achievement_state=removed. |
| `skipped_count` | int unsigned | Members already had a row (in_progress / completed / claimed / expired) — INSERT IGNORE preserved their existing state. |
| `error_message` | varchar(500) | Error message if status=failed · 可空 |
| `started_at` | timestamp | When processing started (used by stuck-job recovery: started_at < NOW() - stuckJobTimeoutSecs → reset to ready). · 可空 |
| `completed_at` | timestamp | When processing completed or failed · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_campaign_active`:campaign_id, active_marker (UNIQUE)
- `idx_status`:status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
