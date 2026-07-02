---
id: tbl_promo_t_cd_camp_referral_applied_reward_relation
object_type: Table
name: referral applied reward relation (t_cd_camp_referral_applied_reward_relation)
aliases: [t_cd_camp_referral_applied_reward_relation, promo.t_cd_camp_referral_applied_reward_relation]
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

# referral applied reward relation (t_cd_camp_referral_applied_reward_relation)

## 用途
物理表 `promo.t_cd_camp_referral_applied_reward_relation`,主键 `id`。referral applied reward relation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `applied_reward_id` | char(32) | applied reward id |
| `campaign_id` | char(32) | campaign id |
| `referee_id` | char(32) | referee id |
| `referee_type` | varchar(15) | referee type : PromoUnique|PayByUnique|PlatformUnique |
| `referral_id` | char(32) | referral id |
| `referral_type` | varchar(15) | referral type: PromoUnique|PayByUnique|PlatformUnique |
| `kind` | varchar(20) | kind: StartBinding|BindingResult|FinishKYC|FinishRemittance|RefereeGetReward|ReferralGetReward |
| `referral_code` | varchar(14) | referral code · 可空 |
| `status` | char | status: 0: failed, 1: success · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_applied_reward_id`:applied_reward_id
- `idx_campaign_id`:campaign_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
