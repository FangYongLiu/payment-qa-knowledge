---
id: tbl_loyalty_t_campaign_started_jobs
object_type: Table
name: Job queue for campaign_started event worker (one job per campaign+audience pair) (t_campaign_started_jobs)
aliases: [t_campaign_started_jobs, loyalty.t_campaign_started_jobs]
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

# Job queue for campaign_started event worker (one job per campaign+audience pair) (t_campaign_started_jobs)

## 用途
物理表 `loyalty.t_campaign_started_jobs`,主键 `id`。Job queue for campaign_started event worker (one job per campaign+audience pair)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `campaign_id` | bigint unsigned | FK to t_campaigns.id (local) |
| `audience_id` | bigint unsigned | FK to t_audiences.id (local) |
| `reason` | varchar(64) | Why enqueued: campaign_synced | users_added |
| `status` | varchar(20) | Job status: pending|processing|done|failed |
| `created_at` | timestamp | When job was enqueued |
| `processed_at` | timestamp | When job was last processed · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_campaign_audience`:campaign_id, audience_id (UNIQUE)
- `idx_status_created`:created_at, status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
