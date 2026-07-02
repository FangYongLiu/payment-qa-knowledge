---
id: tbl_promo_t_cd_camp_bot_vip_conf
object_type: Table
name: bot vip conf (t_cd_camp_bot_vip_conf)
aliases: [t_cd_camp_bot_vip_conf, promo.t_cd_camp_bot_vip_conf]
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

# bot vip conf (t_cd_camp_bot_vip_conf)

## 用途
物理表 `promo.t_cd_camp_bot_vip_conf`,主键 `id`。bot vip conf。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `merchant_id` | varchar(32) | merchant id |
| `campaign_id` | varchar(32) | campaign id |
| `title` | varchar(128) | bot vip airdrop title |
| `pname` | varchar(128) | product name |
| `pid` | varchar(64) | product id |
| `max_audiences` | int | max audiences |
| `reward_count` | int | reward count |
| `description` | varchar(1024) | description · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
