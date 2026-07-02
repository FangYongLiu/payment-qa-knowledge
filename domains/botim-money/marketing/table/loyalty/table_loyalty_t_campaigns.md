---
id: tbl_loyalty_t_campaigns
object_type: Table
name: Campaign cache from Talon.One (t_campaigns)
aliases: [t_campaigns, loyalty.t_campaigns]
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

# Campaign cache from Talon.One (t_campaigns)

## 用途
物理表 `loyalty.t_campaigns`,主键 `id`。Campaign cache from Talon.One。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `talon_campaign_id` | int | Source: Talon Campaign.id |
| `talon_application_id` | int | Source: Talon Campaign.applicationId |
| `talon_ruleset_id` | int | Source: Talon Campaign.activeRulesetId · 可空 |
| `talon_updated` | datetime(6) | Source: Talon Campaign.updated timestamp - for change detection · 可空 |
| `name` | varchar(100) | Source: Talon Campaign.name |
| `description` | varchar(150) | Source: Talon Campaign.description · 可空 |
| `state` | varchar(50) | Source: Talon Campaign.state (enabled, disabled, archived, running, scheduled, expired, staged) |
| `campaign_type` | varchar(50) | Source: Talon Campaign.type (cartItem, advanced) · 可空 |
| `features` | varchar(150) | Source: Talon Campaign.features JSON array (coupons, referrals, loyalty, giveaways, achievements) · 可空 |
| `start_time` | timestamp | Source: Talon Campaign.startTime (optional) · 可空 |
| `end_time` | timestamp | Source: Talon Campaign.endTime (optional) · 可空 |
| `tags` | varchar(200) | Source: Talon Campaign.tags JSON array · 可空 |
| `attributes` | varchar(750) | Source: Talon Campaign.attributes JSON - contains display metadata (reward_type, achievement_type, cta_*, reward_*, etc.) · 可空 |
| `campaign_level_budget` | decimal(15, 2) | Source: Talon Campaign.attributes.campaign_level_budget. Unit follows reward type (fiat for cashback, count for VIP/raffle). NULL = enforcement disabled. · 可空 |
| `session_level_budget` | decimal(15, 2) | Source: Talon Campaign.attributes.session_level_budget. NULL = no session cap. Only honored when cashback_formula_type=percentage (PM item 2). · 可空 |
| `cashback_formula_type` | varchar(15) | Source: Talon Campaign.attributes.cashback_formula_type. Values: percentage | fixed. NULL = treat as fixed (safe default; no session-cap applied). · 可空 |
| `activation_type` | varchar(20) | standard | follow_up |
| `display_priority` | int | Local field: Display order on homepage (lower = higher priority) |
| `is_featured` | tinyint(1) | Local field: Show as featured campaign on homepage |
| `synced_at` | timestamp | Local field: Last sync from Talon.One Management API · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_campaigns_talon_id`:talon_campaign_id (UNIQUE)
- `idx_campaigns_display`:start_time, end_time

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
