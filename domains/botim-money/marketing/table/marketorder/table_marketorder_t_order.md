---
id: tbl_marketorder_t_order
object_type: Table
name: 订单表 (t_order)
aliases: [t_order, marketorder.t_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketorder schema DDL
tags: [marketing, marketorder]
sensitivity: normal
related_services: []
---

# 订单表 (t_order)

## 用途
物理表 `marketorder.t_order`,主键 `order_no`。订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_no` | bigint(18) | 订单编号 |
| `request_order_no` | varchar(64) | 请求订单号 · 可空 |
| `order_type` | varchar(3) | 订单类型：1:普通订单 2:话费订单 |
| `customer_id` | varchar(32) | 下单人id · 可空 |
| `customer_uid` | varchar(32) | 下单人uid · 可空 |
| `order_amount` | decimal(15, 4) | 订单金额 |
| `discount_amount` | decimal(15, 4) | 折扣金额 · 可空 |
| `refund_amount` | decimal(15, 4) | 退款金额 · 可空 |
| `currency` | varchar(10) | 币种 · 可空 |
| `order_status` | varchar(16) | 待补 · 可空 |
| `receive_time` | timestamp | 收货时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `pay_method` | varchar(200) | 支付方式 · 可空 |
| `platform_type` | varchar(12) | 平台类型 · 可空 |
| `partner_id` | varchar(20) | 平台ID · 可空 |
| `payer_partner_id` | varchar(32) | 付款人平台id · 可空 |
| `biz_product_code` | varchar(12) | 业务产品码 · 可空 |
| `refund_time` | timestamp | 退款时间 · 可空 |
| `gmt_paid` | timestamp | 支付时间 · 可空 |
| `payment_no` | bigint(18) | 支付订单号 · 可空 |
| `refund_no` | bigint(18) | 退款订单号 · 可空 |
| `settle_no` | bigint(18) | 结算订单号 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `extends_info` | varchar(512) | 额外字段 · 可空 |
| `order_source` | varchar(30) | 订单来源 · 可空 |
| `unity_result_code` | varchar(50) | 统一返回码 · 可空 |

## 主键 / 索引
- 主键:`order_no`
- `idx_customer_id`:customer_id
- `idx_gmt_modified`:gmt_modified
- `idx_payment_no`:payment_no
- `idx_refund_no`:refund_no
- `idx_request_order_no`:request_order_no
- `idx_settle_no`:settle_no

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
