---
id: tbl_afis_t_aifi_order_item
object_type: Table
name: AiFi pushed order item (t_aifi_order_item)
aliases: [t_aifi_order_item, afis.t_aifi_order_item]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: afis schema DDL
tags: [risk, afis]
sensitivity: normal
related_services: []
---

# AiFi pushed order item (t_aifi_order_item)

## 用途
物理表 `afis.t_aifi_order_item`,主键 `id`。AiFi pushed order item。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `order_id` | char(32) | t_aifi_order id |
| `oiid` | varchar(50) | AiFi Order Item ID · 可空 |
| `name` | varchar(255) | order item name |
| `total_tax` | char(15) | total tax |
| `subtotal_price` | char(15) | subtotal tax |
| `total_price` | char(15) | total price |
| `barcode` | char(32) | order item barcode |
| `category` | char(20) | order item category |
| `thumbnail` | varchar(255) | order item thumbnail |
| `external_id` | varchar(50) | card last four digits |
| `quantity` | int | items quantity |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
