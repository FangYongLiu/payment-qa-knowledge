---
id: tbl_marketorder_t_order_goods
object_type: Table
name: 订单商品明细 (t_order_goods)
aliases: [t_order_goods, marketorder.t_order_goods]
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

# 订单商品明细 (t_order_goods)

## 用途
物理表 `marketorder.t_order_goods`,主键 `id`。订单商品明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `order_no` | bigint(18) | 订单编号 |
| `goods_code` | varchar(16) | 商品编号 |
| `sku_code` | varchar(16) | 商品SKU编号 · 可空 |
| `goods_name` | varchar(100) | 商品名称 · 可空 |
| `sku_info` | varchar(150) | 商品SKU信息 · 可空 |
| `goods_count` | int(10) | 商品数量 · 可空 |
| `goods_price` | decimal(15, 4) | 商品价格 · 可空 |
| `face_value` | decimal(15, 4) | 面值 · 可空 |
| `goods_value` | decimal(15, 4) | 商品价值 · 可空 |
| `voucher_no` | varchar(32) | 虚拟商品凭证号 · 可空 |
| `currency` | varchar(10) | 币种 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `int_currency` | varchar(10) | 国际币种 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_goods_sku_code`:goods_code, sku_code
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
