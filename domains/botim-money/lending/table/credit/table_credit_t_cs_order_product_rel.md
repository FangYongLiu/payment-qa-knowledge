---
id: tbl_credit_t_cs_order_product_rel
object_type: Table
name: t_cs_order_product_rel (t_cs_order_product_rel)
aliases: [t_cs_order_product_rel, credit.t_cs_order_product_rel]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# t_cs_order_product_rel (t_cs_order_product_rel)

## 用途
物理表 `credit.t_cs_order_product_rel`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `order_no` | varchar(64) | 订单号 |
| `product_id` | int | 关联的产品id |
| `external_tif` | decimal(10, 4) | 外部传入的total_interest_fee · 可空 |
| `external_info` | varchar(100) | product_external_info |

## 主键 / 索引
- 主键:`id`
- `uk_on`:order_no (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
