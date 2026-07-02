---
id: tbl_promo_t_cd_rewa_refund_discount_sku
object_type: Table
name: refund discount sku (t_cd_rewa_refund_discount_sku)
aliases: [t_cd_rewa_refund_discount_sku, promo.t_cd_rewa_refund_discount_sku]
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

# refund discount sku (t_cd_rewa_refund_discount_sku)

## 用途
物理表 `promo.t_cd_rewa_refund_discount_sku`,主键 `id`。refund discount sku。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `applied_reward_id` | varchar(32) | reward conf id |
| `refund_reward_id` | varchar(32) | refund reward id |
| `sku_id` | varchar(64) | sku id |
| `merchandise_id` | varchar(64) | merchandise id |
| `merchandise_kind` | varchar(512) | merchandise kind |
| `refund_amount` | decimal(19, 4) | refund amount |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
