---
id: tbl_loyalty_t_user_achievements_archive
object_type: Table
name: Archived user achievement progress. Append-only. (t_user_achievements_archive)
aliases: [t_user_achievements_archive, loyalty.t_user_achievements_archive]
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

# Archived user achievement progress. Append-only. (t_user_achievements_archive)

## 用途
物理表 `loyalty.t_user_achievements_archive`,主键 `id`。Archived user achievement progress. Append-only.。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Original t_user_achievements.id (not auto-increment) |
| `user_id` | bigint unsigned | FK to t_users.id |
| `campaign_id` | bigint unsigned | FK to t_campaigns.id |
| `achievement_id` | bigint unsigned | Local FK: Specific achievement being tracked · 可空 |
| `enrolled_at` | timestamp | When user was enrolled locally (copied from source) · 可空 |
| `enrollment_source` | varchar(15) | automatic|manual|talon_effect|api |
| `current_progress` | decimal(15, 6) | Talon AchievementProgress.progress |
| `target_value` | decimal(15, 6) | Talon AchievementProgress.target |
| `progress_percentage` | decimal(5, 2) | LEAST((current_progress / target_value) * 100, 100) |
| `achievement_state` | varchar(15) | new|in_progress|completed|expired |
| `completed_at` | timestamp | When user completed · 可空 |
| `reward_claimed_at` | timestamp | When reward was claimed/issued · 可空 |
| `reward_credit_status` | varchar(15) | pending|processing|credited|failed · 可空 |
| `expires_at` | timestamp | Achievement period or Talon AchievementProgress.endDate · 可空 |
| `activated_at` | datetime(3) | When follow-up quest was activated for this user · 可空 |
| `personal_expires_at` | datetime(3) | Per-user expiry = activated_at + achievement.period (follow-up only) · 可空 |
| `last_progress_at` | timestamp | When progress was last updated from Talon · 可空 |
| `talon_session_id` | varchar(100) | Last Talon.One session ID that updated progress · 可空 |
| `created_at` | timestamp | Original record creation timestamp (copied from source) · 可空 |
| `updated_at` | timestamp | Original record last update timestamp (copied; no ON UPDATE) · 可空 |
| `archived_at` | timestamp | When the row was archived |

## 主键 / 索引
- 主键:`id`
- `idx_archive_archived_at`:archived_at
- `idx_archive_campaign`:campaign_id
- `idx_archive_user`:user_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
