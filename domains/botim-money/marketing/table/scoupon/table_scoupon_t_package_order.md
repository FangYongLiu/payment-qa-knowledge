---
id: tbl_scoupon_t_package_order
object_type: Table
name: 套餐订单 (t_package_order)
aliases: [t_package_order, scoupon.t_package_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: scoupon schema DDL
tags: [marketing, scoupon]
sensitivity: normal
related_services: []
---

# 套餐订单 (t_package_order)

## 用途
物理表 `scoupon.t_package_order`,主键 `id`。套餐订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键id |
| `order_no` | varchar(32) | 交易订单号 |
| `merchant_no` | varchar(32) | 商户订单号 |
| `biz_product_code` | varchar(32) | 业务产品码 · 可空 |
| `payer_id` | varchar(32) | 付款人 |
| `partner_id` | varchar(32) | 平台方 |
| `source` | varchar(32) | 来源平台 |
| `order_amount` | decimal(19, 4) | 订单金额 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `order_status` | varchar(12) | 订单状态 |
| `is_refund` | varchar(12) | 是否退款 · 可空 |
| `refund_order_no` | varchar(32) | 退款订单号 · 可空 |
| `relation_id` | bigint | 关联id · 可空 |
| `relation_type` | varchar(32) | 关联类型 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |
| `paid_time` | timestamp | 支付完成时间 · 可空 |
| `finish_time` | timestamp | 交易完成时间 · 可空 |
| `refund_time` | timestamp | 退款完成时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
