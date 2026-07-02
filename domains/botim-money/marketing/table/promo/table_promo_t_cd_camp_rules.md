---
id: tbl_promo_t_cd_camp_rules
object_type: Table
name: campaign rules (t_cd_camp_rules)
aliases: [t_cd_camp_rules, promo.t_cd_camp_rules]
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

# campaign rules (t_cd_camp_rules)

## 用途
物理表 `promo.t_cd_camp_rules`,主键 `id`。campaign rules。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `conf_type` | varchar(16) | PromoCode|Referral|Trigger |
| `conf_id` | varchar(32) | camp conf id |
| `kind` | varchar(128) | the kind of rules |
| `rules` | varchar(2048) | the rules extend of campaign |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
