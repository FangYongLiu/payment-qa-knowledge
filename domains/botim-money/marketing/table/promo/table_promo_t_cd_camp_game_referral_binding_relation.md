---
id: tbl_promo_t_cd_camp_game_referral_binding_relation
object_type: Table
name: infr game referral binding relation (t_cd_camp_game_referral_binding_relation)
aliases: [t_cd_camp_game_referral_binding_relation, promo.t_cd_camp_game_referral_binding_relation]
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

# infr game referral binding relation (t_cd_camp_game_referral_binding_relation)

## 用途
物理表 `promo.t_cd_camp_game_referral_binding_relation`,主键 `id`。infr game referral binding relation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `code_id` | varchar(32) | code id |
| `code` | varchar(32) | code |
| `referee_id` | varchar(32) | referee id |
| `referee_type` | varchar(15) | referee type:PromoUnique|PayByUnique|PlatformUnique |
| `referrer_id` | varchar(32) | referrer id |
| `referrer_type` | varchar(15) | referrer type:PromoUnique|PayByUnique|PlatformUnique |
| `kind` | varchar(15) | kind:Inactive|Active|Alone |
| `status` | varchar(15) | status:Init|Kyc|Remittance|Cancel |
| `is_deleted` | tinyint(1) | is deleted |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
