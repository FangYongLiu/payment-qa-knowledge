---
id: tbl_marketgoods_t_goods_sku
object_type: Table
name: 商品SKU信息表 (t_goods_sku)
aliases: [t_goods_sku, marketgoods.t_goods_sku]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketgoods schema DDL
tags: [marketing, marketgoods]
sensitivity: normal
related_services: []
---

# 商品SKU信息表 (t_goods_sku)

## 用途
物理表 `marketgoods.t_goods_sku`,主键 `id`。商品SKU信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `goods_code` | varchar(16) | 商品编号 · 可空 |
| `sku_code` | varchar(16) | sku编号 |
| `sku_info` | varchar(250) | sku信息 · 可空 |
| `sku_price` | decimal(15, 4) | sku价格 · 可空 |
| `face_value` | decimal(15, 4) | 面值 · 可空 |
| `origin_price` | decimal(15, 4) | 原价 |
| `sell_price` | decimal(15, 4) | 促销价 |
| `currency` | varchar(10) | 币种 · 可空 |
| `status` | varchar(3) | 状态（1：上架 0：下架） |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `extension` | varchar(250) | 额外信息 · 可空 |
| `sku_price_currency` | varchar(12) | 价值币种 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_sku_code`:sku_code (UNIQUE)
- `idx_goods_code`:goods_code

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
