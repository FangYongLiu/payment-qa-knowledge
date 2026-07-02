---
id: tbl_promo_t_cd_rewa_conf_discount
object_type: Table
name: extra reward conf for discount (t_cd_rewa_conf_discount)
aliases: [t_cd_rewa_conf_discount, promo.t_cd_rewa_conf_discount]
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

# extra reward conf for discount (t_cd_rewa_conf_discount)

## 用途
物理表 `promo.t_cd_rewa_conf_discount`,主键 `id`。extra reward conf for discount。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `min_amount` | decimal(19, 4) | the min amount for discount |
| `max_amount` | decimal(19, 4) | the max amount for discount |
| `budget_amount` | decimal(19, 4) | the budget amount for discount |
| `budget_currency` | char(3) | the budget currency for discount |
| `budget_vault_id` | varchar(32) | the budget vault id for discount |
| `create_at` | timestamp | the create time of the discount |
| `update_at` | timestamp | the update time of the discount |
| `hidden_from_user` | char | whether the discount is hidden from user (Y/N) · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
