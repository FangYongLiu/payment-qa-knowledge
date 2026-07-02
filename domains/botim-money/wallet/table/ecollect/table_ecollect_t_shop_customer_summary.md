---
id: tbl_ecollect_t_shop_customer_summary
object_type: Table
name: Shop x Customer relation aggregate (t_shop_customer_summary)
aliases: [t_shop_customer_summary, ecollect.t_shop_customer_summary]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ecollect schema DDL
tags: [wallet, ecollect]
sensitivity: normal
related_services: []
---

# Shop x Customer relation aggregate (t_shop_customer_summary)

## 用途
物理表 `ecollect.t_shop_customer_summary`,主键 `id`。Shop x Customer relation aggregate。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | PK |
| `shop_id` | bigint(21) | Shop ID |
| `user_id` | varchar(8) | Botim UID |
| `first_purchased_at` | timestamp | First PAID timestamp (immutable) · 可空 |
| `last_purchased_at` | timestamp | Latest PAID timestamp · 可空 |
| `purchase_order_count` | int(8) | Cumulative PAID order count |
| `purchase_count_30d` | int(8) | PAID orders in last 30 days (daily cron) |
| `purchase_count_30d_at` | timestamp | Last 30d recompute time · 可空 |
| `total_paid_amount` | decimal(18, 2) | Cumulative paid amount |
| `total_refunded_amount` | decimal(18, 2) | Cumulative refunded amount |
| `view_product_count` | int(8) | Cumulative VIEW_PRODUCT events |
| `last_viewed_at` | timestamp | Latest view timestamp · 可空 |
| `loyalty_tag` | varchar(20) | NEW / REPEAT / LOYAL / LAPSED · 可空 |
| `loyalty_tag_version` | varchar(10) | Rule version · 可空 |
| `loyalty_tag_computed_at` | timestamp | 待补 · 可空 |
| `create_time` | timestamp | Relation first-seen time |
| `update_time` | timestamp | Last write time · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_shop_user`:shop_id, user_id (UNIQUE)
- `idx_shop_id`:shop_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
