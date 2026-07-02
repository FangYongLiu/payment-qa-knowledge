---
id: tbl_loyalty_t_campaign_started_events
object_type: Table
name: Tracks which users have received campaign_started events (one row per user+campaign) (t_campaign_started_events)
aliases: [t_campaign_started_events, loyalty.t_campaign_started_events]
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

# Tracks which users have received campaign_started events (one row per user+campaign) (t_campaign_started_events)

## 用途
物理表 `loyalty.t_campaign_started_events`,主键 `id`。Tracks which users have received campaign_started events (one row per user+campaign)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `user_id` | bigint unsigned | FK to t_users.id |
| `campaign_id` | bigint unsigned | FK to t_campaigns.id (local) |
| `integration_id` | varchar(105) | Talon.One integration ID (cached to avoid join; matches t_users.integration_id) |
| `sent_at` | timestamp | When event was sent to Talon.One |

## 主键 / 索引
- 主键:`id`
- `uk_user_campaign`:user_id, campaign_id (UNIQUE)
- `idx_campaign_sent`:campaign_id, sent_at

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
