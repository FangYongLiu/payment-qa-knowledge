---
id: tbl_loyalty_t_raffle_entries_2026_01
object_type: Table
name: Raffle entries from loyalty campaigns - 2026-01 (t_raffle_entries_2026_01)
aliases: [t_raffle_entries_2026_01, loyalty.t_raffle_entries_2026_01]
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

# Raffle entries from loyalty campaigns - 2026-01 (t_raffle_entries_2026_01)

## 用途
物理表 `loyalty.t_raffle_entries_2026_01`,主键 `id`。Raffle entries from loyalty campaigns - 2026-01。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `user_id` | bigint unsigned | FK to t_users.id |
| `ucid` | varchar(50) | User UCID |
| `campaign_id` | bigint unsigned | FK to t_campaigns.id · 可空 |
| `achievement_id` | bigint unsigned | FK to t_achievements.id · 可空 |
| `source_event_id` | varchar(100) | Event that triggered entry |
| `created_at` | timestamp | Record creation timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_raffle_campaign`:campaign_id
- `idx_raffle_created`:created_at
- `idx_raffle_ucid`:ucid

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
