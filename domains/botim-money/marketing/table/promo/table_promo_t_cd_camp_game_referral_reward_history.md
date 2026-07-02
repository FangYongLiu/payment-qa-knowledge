---
id: tbl_promo_t_cd_camp_game_referral_reward_history
object_type: Table
name: game referral reward history (t_cd_camp_game_referral_reward_history)
aliases: [t_cd_camp_game_referral_reward_history, promo.t_cd_camp_game_referral_reward_history]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# game referral reward history (t_cd_camp_game_referral_reward_history)

## 用途
物理表 `promo.t_cd_camp_game_referral_reward_history`,主键 `id`。game referral reward history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `conf_id` | varchar(32) | conf id |
| `task_conf_id` | varchar(32) | task conf id |
| `relation_id` | varchar(32) | relation id |
| `kind` | varchar(15) | kind:Kyc|Remittance|CompletedTask |
| `referrer_id` | varchar(32) | referrer id |
| `referrer_type` | varchar(15) | referrer type:PromoUnique|PayByUnique|PlatformUnique |
| `customer_id` | varchar(32) | referrer id |
| `customer_type` | varchar(15) | referrer type:PromoUnique|PayByUnique|PlatformUnique |
| `reward_id` | varchar(32) | reward id |
| `reward_type` | varchar(10) | reward type:Cashback|BotVip |
| `status` | varchar(15) | status:Init|Pending|Redeemed|Failed |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
