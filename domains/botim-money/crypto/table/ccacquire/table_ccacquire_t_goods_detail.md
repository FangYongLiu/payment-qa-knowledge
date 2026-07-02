---
id: tbl_ccacquire_t_goods_detail
object_type: Table
name: 商品信息 (t_goods_detail)
aliases: [t_goods_detail, ccacquire.t_goods_detail]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccacquire schema DDL
tags: [crypto, ccacquire]
sensitivity: normal
related_services: []
---

# 商品信息 (t_goods_detail)

## 用途
物理表 `ccacquire.t_goods_detail`,主键 `global_id`。商品信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `goods_id` | varchar(200) | 待补 · 可空 |
| `goods_name` | varchar(200) | 待补 · 可空 |
| `price` | decimal(23, 8) | 待补 · 可空 |
| `price_currency_code` | varchar(32) | 币种 · 可空 |
| `quantity` | decimal(23, 8) | 待补 · 可空 |
| `goods_category` | varchar(200) | 待补 · 可空 |
| `categories_tree` | varchar(200) | 待补 · 可空 |
| `body` | varchar(500) | 待补 · 可空 |
| `show_url` | varchar(500) | 待补 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
