---
id: tbl_rnpl_t_property
object_type: Table
name: Housing Information Registration Table (t_property)
aliases: [t_property, rnpl.t_property]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Housing Information Registration Table (t_property)

## 用途
物理表 `rnpl.t_property`,主键 `id`。Housing Information Registration Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `unique_property_id` | varchar(32) | unique id of the property |
| `address` | varchar(255) | address of the house |
| `property_type` | varchar(20) | 待补 |
| `emirate` | varchar(20) | 待补 |
| `property_url` | varchar(255) | 待补 · 可空 |
| `contract_id` | int | contract id |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
