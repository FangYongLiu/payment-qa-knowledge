---
id: tbl_loyalty_t_custom_effects_2026_08
object_type: Table
name: Custom effects from Talon.One - orchestration layer for reward processing - 2026-08 (t_custom_effects_2026_08)
aliases: [t_custom_effects_2026_08, loyalty.t_custom_effects_2026_08]
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

# Custom effects from Talon.One - orchestration layer for reward processing - 2026-08 (t_custom_effects_2026_08)

## 用途
物理表 `loyalty.t_custom_effects_2026_08`,主键 `id`。Custom effects from Talon.One - orchestration layer for reward processing - 2026-08。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key auto-increment · 可空 |
| `user_id` | bigint unsigned | FK to t_users.id |
| `talon_effect_id` | bigint | Effect ID from Talon.One (props.effectId) |
| `talon_campaign_id` | int | Campaign ID that triggered this effect |
| `talon_ruleset_id` | int | Ruleset ID that triggered this effect · 可空 |
| `talon_rule_index` | int | Rule index within the ruleset · 可空 |
| `talon_rule_name` | varchar(200) | Rule name that triggered this effect · 可空 |
| `effect_type` | varchar(50) | Effect type from Talon.One: customEffect |
| `effect_name` | varchar(100) | Custom effect name: cashback, vip_reward, raffle_entry |
| `source_event_id` | varchar(100) | Event ID that triggered this effect |
| `cashback_transaction_id` | bigint unsigned | FK to t_cashback_transactions (if effect_name=cashback) · 可空 |
| `vip_subscription_id` | bigint unsigned | FK to t_vip_subscriptions (if effect_name=vip_reward) · 可空 |
| `raffle_entry_id` | bigint unsigned | FK to t_raffle_entries (if effect_name=Raffle Entry) · 可空 |
| `gold_reward_id` | bigint unsigned | FK to t_gold_reward_transactions_* (if effect_name=Gold Reward or Silver Reward) · 可空 |
| `status` | varchar(20) | Processing status: pending|processing|completed|failed|permanently_failed|skipped |
| `error_code` | varchar(50) | Error code if failed · 可空 |
| `error_message` | varchar(1000) | Error message if failed · 可空 |
| `retry_count` | int unsigned | Number of retry attempts |
| `max_retries` | int unsigned | Maximum retry attempts |
| `next_retry_at` | timestamp | When next retry should be attempted · 可空 |
| `completed_at` | timestamp | When processing completed successfully · 可空 |
| `created_at` | timestamp | Record creation timestamp |
| `updated_at` | timestamp | Record last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_custom_effects_idempotency`:user_id, talon_campaign_id, source_event_id (UNIQUE)
- `idx_custom_effects_campaign`:talon_campaign_id, effect_name, status
- `idx_custom_effects_retry`:next_retry_at, status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
