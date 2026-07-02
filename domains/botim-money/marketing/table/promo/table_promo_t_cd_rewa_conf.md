---
id: tbl_promo_t_cd_rewa_conf
object_type: Table
name: reward conf (t_cd_rewa_conf)
aliases: [t_cd_rewa_conf, promo.t_cd_rewa_conf]
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

# reward conf (t_cd_rewa_conf)

## 用途
物理表 `promo.t_cd_rewa_conf`,主键 `id`。reward conf。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `reward_type` | char(10) | enums: Cashback|Discount|BotVip |
| `title` | varchar(60) | title of the campaign reward conf |
| `description` | varchar(255) | the reward description · 可空 |
| `max_audience` | bigint | the max allowed audience number for this reward conf · 可空 |
| `reward_count` | bigint | the max count for this reward delivered to a customer · 可空 |
| `start_at` | timestamp | the start time of the reward conf |
| `end_at` | timestamp | the end time of the reward conf |
| `create_at` | timestamp | the create time of the reward conf |
| `update_at` | timestamp | the update time of the reward conf |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
