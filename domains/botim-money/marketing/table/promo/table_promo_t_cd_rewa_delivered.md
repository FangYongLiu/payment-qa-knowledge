---
id: tbl_promo_t_cd_rewa_delivered
object_type: Table
name: delivered reward (t_cd_rewa_delivered)
aliases: [t_cd_rewa_delivered, promo.t_cd_rewa_delivered]
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

# delivered reward (t_cd_rewa_delivered)

## 用途
物理表 `promo.t_cd_rewa_delivered`,主键 `id`。delivered reward。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `conf_id` | varchar(32) | reward conf id |
| `kind` | varchar(10) | Enums: Cashback|Discount|BotVip |
| `title` | varchar(100) | title of the campaign reward conf |
| `description` | varchar(255) | the reward description (in conf) · 可空 |
| `customer_id` | varchar(32) | customer id · 可空 |
| `customer_uid` | varchar(32) | customer uid · 可空 |
| `customer_payby_mid` | varchar(64) | customer payby mid · 可空 |
| `merchant_id` | varchar(32) | merchant id |
| `status` | varchar(20) | Delivered|Locked|Redeeming|RedeemingPending|Redeemed|RedeemFail · 可空 |
| `create_at` | timestamp | the create time of the delivered reward |
| `update_at` | timestamp | the update time of the delivered reward |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
