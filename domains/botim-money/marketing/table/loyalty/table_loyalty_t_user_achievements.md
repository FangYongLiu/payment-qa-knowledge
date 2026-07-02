---
id: tbl_loyalty_t_user_achievements
object_type: Table
name: User progress on achievements within campaigns (t_user_achievements)
aliases: [t_user_achievements, loyalty.t_user_achievements]
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

# User progress on achievements within campaigns (t_user_achievements)

## 用途
物理表 `loyalty.t_user_achievements`,主键 `id`。User progress on achievements within campaigns。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `user_id` | bigint unsigned | FK to t_users.id |
| `campaign_id` | bigint unsigned | FK to t_campaigns.id |
| `achievement_id` | bigint unsigned | Local FK: Specific achievement being tracked · 可空 |
| `enrolled_at` | timestamp | Local field: When user was enrolled locally |
| `enrollment_source` | varchar(15) | Local field: How enrollment was triggered: automatic|manual|talon_effect|api |
| `current_progress` | decimal(15, 6) | Source: Talon AchievementProgress.progress (from inventory API) |
| `target_value` | decimal(15, 6) | Source: Talon AchievementProgress.target (from inventory API) |
| `progress_percentage` | decimal(5, 2) | Calculated in app: LEAST((current_progress / target_value) * 100, 100) |
| `achievement_state` | varchar(15) | Derived from: Talon AchievementProgress.status: new|in_progress|completed|expired|claimed (not_started→new, inprogress→in_progress) |
| `completed_at` | timestamp | Local field: When user completed (set when achievement_state changes to completed) · 可空 |
| `reward_claimed_at` | timestamp | Local field: When reward was claimed/issued · 可空 |
| `reward_credit_status` | varchar(15) | Local field: Reward fulfillment status: pending|processing|credited|failed, updated by event processor after custom_effects processing · 可空 |
| `expires_at` | timestamp | Derived from: Achievement period or Talon AchievementProgress.endDate · 可空 |
| `activated_at` | datetime(3) | Follow-up activation timestamp (NULL for standard) · 可空 |
| `personal_expires_at` | datetime(3) | Follow-up per-user expiry = activated_at + period (NULL for standard) · 可空 |
| `last_progress_at` | timestamp | Local field: When progress was last updated from Talon · 可空 |
| `talon_session_id` | varchar(100) | Source: Last Talon.One session ID that updated progress · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_user_achievements`:user_id, campaign_id, achievement_id (UNIQUE)
- `idx_user_achievements_campaign`:campaign_id
- `idx_user_achievements_expires`:expires_at
- `idx_user_achievements_state`:user_id, achievement_state
- `idx_user_achievements_state_at`:achievement_state, personal_expires_at, id
- `idx_user_achievements_user`:user_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
