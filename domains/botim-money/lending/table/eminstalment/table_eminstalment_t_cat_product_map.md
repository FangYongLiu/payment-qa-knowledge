---
id: tbl_eminstalment_t_cat_product_map
object_type: Table
name: 商品品类与可使用的分期产品映射 (t_cat_product_map)
aliases: [t_cat_product_map, eminstalment.t_cat_product_map]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 商品品类与可使用的分期产品映射 (t_cat_product_map)

## 用途
物理表 `eminstalment.t_cat_product_map`,主键 `id`。商品品类与可使用的分期产品映射。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `cat_id` | varchar(32) | 商品品类id |
| `cat_name` | varchar(64) | 品类名 |
| `cat_priority` | int | Cat 优先级。当查找多个cat对应的最优产品时，根据cat的优先级取优先级最高的cat对应的产品 |
| `min_price` | decimal(15, 2) | 购物金额条件，最低值 |
| `max_price` | decimal(15, 2) | 购物金额条件，最大值 |
| `product_id` | int | 商品品类可使用的分期产品id，对应t_product表的id |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
