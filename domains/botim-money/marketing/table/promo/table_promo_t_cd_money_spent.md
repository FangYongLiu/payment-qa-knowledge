---
id: tbl_promo_t_cd_money_spent
object_type: Table
name: money spent (t_cd_money_spent)
aliases: [t_cd_money_spent, promo.t_cd_money_spent]
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

# money spent (t_cd_money_spent)

## 用途
物理表 `promo.t_cd_money_spent`,主键 `id`。money spent。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `in_campaign_id` | char(32) | campaign id |
| `in_batch_id` | char(32) | batch id |
| `from_owner_id` | char(32) | from owner id |
| `to_customer_id` | char(32) | to customer id |
| `create_at` | timestamp | create time |
| `amount` | decimal(19, 4) | amount of the customer reward spent |
| `currency` | char(3) | currency of the customer reward spent |

## 主键 / 索引
- 主键:`id`
- `idx_in_campaign_id`:in_campaign_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
