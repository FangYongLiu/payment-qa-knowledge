---
id: tbl_loyalty_t_achievements
object_type: Table
name: Achievement definitions within campaigns (t_achievements)
aliases: [t_achievements, loyalty.t_achievements]
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

# Achievement definitions within campaigns (t_achievements)

## 用途
物理表 `loyalty.t_achievements`,主键 `id`。Achievement definitions within campaigns。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `campaign_id` | bigint unsigned | Local FK: Parent campaign |
| `talon_achievement_id` | varchar(100) | Source: Talon Achievement.id (format: campaignId-achievementId) |
| `name` | varchar(100) | Source: Talon Achievement.name |
| `title` | varchar(100) | Source: Talon Achievement.title · 可空 |
| `achievement_description` | varchar(300) | Display: Parsed achievement description from metadata · 可空 |
| `description` | varchar(1500) | Source: Talon Achievement.description - contains metadata JSON (reward_type, achievement_type, cta_*, reward_*, is_primary) · 可空 |
| `achievement_type` | varchar(15) | Derived from: Talon tracking type: counter|accumulator|milestone |
| `target_value` | decimal(15, 6) | Source: Talon Achievement.target |
| `target_unit` | varchar(50) | Source: Talon Achievement.description JSON → target_unit, or default based on achievement_type · 可空 |
| `period` | varchar (20) | Source: Talon Achievement.period (15D, 1M, 3M, etc.) · 可空 |
| `activation_policy` | varchar(20) | Source: Talon Achievement.activationPolicy: user_action|fixed_schedule - determines how achievement starts/ends/resets · 可空 |
| `fixed_start_date` | timestamp | Source: Talon Achievement.fixedStartDate - start date when activationPolicy=fixed_schedule · 可空 |
| `end_date` | timestamp | Source: Talon Achievement.endDate - absolute end date, customers cannot participate after this · 可空 |
| `recurrence_policy` | varchar(20) | Source: Talon Achievement.recurrencePolicy: no_recurrence|on_expiration|on_completion · 可空 |
| `progress_unit_label` | varchar(50) | Derived from: metadata or achievement_type · 可空 |
| `reward_type` | varchar(15) | Derived from: metadata reward_type or campaign rules: cashback|voucher|vip_trial · 可空 |
| `reward_value` | varchar(50) | Display: Reward value with unit (e.g., "15 AED", "10 Days Free") · 可空 |
| `reward_currency` | char(3) | 待补 · 可空 |
| `reward_title` | varchar(200) | Display: Short reward name (e.g., "Cashback Reward") · 可空 |
| `reward_icon` | varchar(512) | Display: Reward icon URL · 可空 |
| `reward_description` | varchar(100) | Display: Detailed reward description · 可空 |
| `reward_terms` | varchar(200) | Display: Terms and conditions for the reward · 可空 |
| `reward_completion_message` | varchar(200) | Display: text shown to the user when the reward is credited (required for reward_type=message, optional otherwise) · 可空 |
| `reward_cta_text` | varchar(100) | Display: CTA button text for completed state (e.g., "View Wallet") · 可空 |
| `reward_cta_link` | varchar(150) | CTA button link on reward page · 可空 |
| `icon_url` | varchar(150) | Derived from: metadata achievement_icon · 可空 |
| `achievement_banner` | varchar(150) | Display: Banner image URL for detail page · 可空 |
| `cta_deeplink` | varchar(150) | Derived from: metadata cta_link · 可空 |
| `campaign_cta_deeplink` | varchar(150) | Display: Campaign-level CTA deeplink (promoted to CampaignInfo.cta_deeplink) · 可空 |
| `campaign_terms_url` | varchar(150) | Campaign T&C URL (from metadata, promoted to campaign level) · 可空 |
| `cta_text` | varchar(50) | Derived from: metadata cta_name · 可空 |
| `is_primary` | tinyint(1) | Display: Primary achievement flag for campaign summary |
| `is_hidden` | tinyint(1) | Local field: Hidden until unlocked |
| `synced_at` | timestamp | Local field: Last sync from Talon.One Management API · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_achievements_talon_id`:talon_achievement_id (UNIQUE)
- `idx_achievements_campaign`:campaign_id
- `idx_achievements_recurrence`:recurrence_policy
- `idx_achievements_timing`:fixed_start_date, end_date

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
