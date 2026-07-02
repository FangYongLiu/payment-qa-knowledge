---
id: tbl_botimsnpl_t_sl_order_promo
object_type: Table
name: t_sl_order_promo (t_sl_order_promo)
aliases: [t_sl_order_promo, botimsnpl.t_sl_order_promo]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# t_sl_order_promo (t_sl_order_promo)

## 用途
物理表 `botimsnpl.t_sl_order_promo`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `order_no` | varchar(64) | order no |
| `user_id` | varchar(20) | user id |
| `campaign_code` | varchar(50) | campaign code · 可空 |
| `coupon_code` | varchar(50) | coupon code · 可空 |
| `campaign_id` | bigint | campaign id · 可空 |
| `coupon_id` | bigint | coupon id · 可空 |
| `original_flat_rate` | decimal(12, 6) | original flat rate |
| `current_flat_rate` | decimal(12, 6) | current flat rate |
| `original_monthly_rate` | decimal(12, 6) | original monthly rate |
| `current_monthly_rate` | decimal(12, 6) | current monthly rate |
| `original_interest_amount` | decimal(15, 2) | original interest amount |
| `current_interest_amount` | decimal(15, 2) | current interest amount |
| `discounted_interest_amount` | decimal(15, 2) | discounted interest amount |
| `ext` | varchar(255) | ext · 可空 |
| `created_time` | timestamp | created time |
| `last_modified` | timestamp | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_order_promo_ordno`:order_no
- `idx_order_promo_usrid`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
