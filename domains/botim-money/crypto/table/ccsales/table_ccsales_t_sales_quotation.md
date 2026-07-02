---
id: tbl_ccsales_t_sales_quotation
object_type: Table
name: 销售报价 (t_sales_quotation)
aliases: [t_sales_quotation, ccsales.t_sales_quotation]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccsales schema DDL
tags: [crypto, ccsales]
sensitivity: normal
related_services: []
---

# 销售报价 (t_sales_quotation)

## 用途
物理表 `ccsales.t_sales_quotation`,主键 `sales_order_id`。销售报价。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `sales_order_id` | bigint | id |
| `market_quote_price` | decimal(23, 8) | 行情-当前市价 |
| `sell_price` | decimal(23, 8) | 行情卖价 |
| `buy_price` | decimal(23, 8) | 行情买价 |
| `real_limit_rate` | decimal(23, 8) | real_limit_rate |
| `limit_rate` | decimal(23, 8) | limit_rate |
| `ocbs_quote_price` | decimal(23, 8) | obcs报价 · 可空 |

## 主键 / 索引
- 主键:`sales_order_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
