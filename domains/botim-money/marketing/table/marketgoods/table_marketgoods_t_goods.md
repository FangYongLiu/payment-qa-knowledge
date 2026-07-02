---
id: tbl_marketgoods_t_goods
object_type: Table
name: 商品表 (t_goods)
aliases: [t_goods, marketgoods.t_goods]
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

# 商品表 (t_goods)

## 用途
物理表 `marketgoods.t_goods`,主键 `id`。商品表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `goods_code` | varchar(16) | 商品编号 |
| `goods_name` | varchar(100) | 商品名称 · 可空 |
| `brand` | varchar(50) | 品牌 · 可空 |
| `top_category_code` | varchar(12) | 顶级品类 · 可空 |
| `sup_category_code` | varchar(12) | 上级品类 · 可空 |
| `category_code` | varchar(12) | 品类 · 可空 |
| `origin_price` | decimal(15, 4) | 原价 |
| `sell_price` | decimal(15, 4) | 促销价 |
| `currency` | varchar(10) | 币种 · 可空 |
| `entity_flag` | tinyint(1) | 是否实物商品 |
| `status` | varchar(3) | 状态（1：下架 2：上架  ） |
| `online_time` | timestamp | 上架时间 · 可空 |
| `offline_time` | timestamp | 下架时间 · 可空 |
| `goods_desc` | varchar(150) | 商品描述 · 可空 |
| `goods_source` | varchar(16) | 商品来源  self:自平台    supplier:供应商 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_goods_code`:goods_code (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
