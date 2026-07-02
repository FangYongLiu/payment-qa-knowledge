---
id: tbl_promo_t_cd_rewa_applied
object_type: Table
name: applied reward (t_cd_rewa_applied)
aliases: [t_cd_rewa_applied, promo.t_cd_rewa_applied]
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

# applied reward (t_cd_rewa_applied)

## 用途
物理表 `promo.t_cd_rewa_applied`,主键 `id`。applied reward。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `delivered_id` | varchar(32) | delivered reward id |
| `conf_id` | varchar(32) | reward conf id |
| `campaign_id` | varchar(32) | campaign id |
| `kind` | char(10) | Enums: Cashback|Discount|BotVip |
| `title` | varchar(100) | title of the applied reward |
| `description` | varchar(255) | the reward description (in conf) · 可空 |
| `customer_id` | varchar(32) | customer id · 可空 |
| `customer_uid` | varchar(32) | customer uid · 可空 |
| `customer_payby_mid` | varchar(64) | customer payby mid · 可空 |
| `merchant_id` | varchar(32) | merchant id |
| `ms_code` | varchar(20) | merchant store code |
| `txn_id` | varchar(64) | transaction id · 可空 |
| `txn_amount` | decimal(19, 4) | transaction amount · 可空 |
| `status` | varchar(20) | Applied|Locked|Redeeming|RedeemingPendingRedeemed|RedeemFail · 可空 |
| `create_at` | timestamp | the create time of the applied reward |
| `update_at` | timestamp | the update time of the applied reward |

## 主键 / 索引
- 主键:`id`
- `idx_campaign_id`:campaign_id
- `idx_campaign_status_customer`:campaign_id, status, customer_id

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
