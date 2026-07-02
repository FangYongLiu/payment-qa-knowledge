---
id: tbl_promo_t_cd_camp_game_referral_task_conf
object_type: Table
name: infr game referral task conf (t_cd_camp_game_referral_task_conf)
aliases: [t_cd_camp_game_referral_task_conf, promo.t_cd_camp_game_referral_task_conf]
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

# infr game referral task conf (t_cd_camp_game_referral_task_conf)

## 用途
物理表 `promo.t_cd_camp_game_referral_task_conf`,主键 `id`。infr game referral task conf。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `campaign_id` | varchar(32) | merchant id |
| `conf_id` | varchar(32) | conf id |
| `title` | varchar(127) | title |
| `description` | varchar(255) | description |
| `start_at` | timestamp | start at |
| `end_at` | timestamp | end at |
| `cta_action` | varchar(255) | cta action · 可空 |
| `kind` | varchar(15) | kind:Kyc|Remittance|CompletedTask |
| `amount` | decimal(19, 4) | amount |
| `limit_count` | int | limit count |
| `sort` | int | order |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
