---
id: tbl_promo_t_cd_camp_referral_relation
object_type: Table
name: t_cd_camp_referral_relation (t_cd_camp_referral_relation)
aliases: [t_cd_camp_referral_relation, promo.t_cd_camp_referral_relation]
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

# t_cd_camp_referral_relation (t_cd_camp_referral_relation)

## 用途
物理表 `promo.t_cd_camp_referral_relation`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | char(32) | campaign id |
| `trigger_key` | varchar(64) | trigger key |
| `beneficiary_type` | varchar(64) | beneficiary type |
| `reward_conf_id` | varchar(32) | reward conf id |
| `reward_type` | char(8) | reward type:Cashback|Discount|BotVip  |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
