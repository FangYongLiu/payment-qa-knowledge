---
id: tbl_marketorder_t_goods_stock
object_type: Table
name: 商品库存表 (t_goods_stock)
aliases: [t_goods_stock, marketorder.t_goods_stock]
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

# 商品库存表 (t_goods_stock)

## 用途
物理表 `marketorder.t_goods_stock`,主键 `id`。商品库存表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `goods_code` | varchar(16) | 商品编号 |
| `sku_code` | varchar(16) | 商品SKU编号 · 可空 |
| `stock_count` | int(10) | 库存数量 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_goods_code`:goods_code

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
