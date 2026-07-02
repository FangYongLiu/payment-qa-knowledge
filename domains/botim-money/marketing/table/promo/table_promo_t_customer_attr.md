---
id: tbl_promo_t_customer_attr
object_type: Table
name: Customers attributes (t_customer_attr)
aliases: [t_customer_attr, promo.t_customer_attr]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# Customers attributes (t_customer_attr)

## 用途
物理表 `promo.t_customer_attr`,主键 `id`。Customers attributes。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `customer_id` | varchar(32) | 待补 |
| `attr_name` | varchar(100) | 待补 |
| `attr_value` | varchar(2000) | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
