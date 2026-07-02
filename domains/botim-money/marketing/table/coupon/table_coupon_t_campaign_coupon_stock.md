---
id: tbl_coupon_t_campaign_coupon_stock
object_type: Table
name: t_campaign_coupon_stock (t_campaign_coupon_stock)
aliases: [t_campaign_coupon_stock, coupon.t_campaign_coupon_stock]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# t_campaign_coupon_stock (t_campaign_coupon_stock)

## 用途
物理表 `coupon.t_campaign_coupon_stock`,主键 `stock_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `stock_id` | bigint | 主键id · 可空 |
| `coupon_id` | bigint | 优惠券id |
| `campaign_id` | bigint | 活动id |
| `relation_id` | bigint | 券库存关联id |
| `default_stock` | int(12) | 默认库存 |
| `weight` | int(10) | 权重 · 可空 |
| `stock` | int(12) | 实际库存 |
| `start_time` | timestamp | 开始时间 · 可空 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `used_stock` | int(12) | 已使用库存 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`stock_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
