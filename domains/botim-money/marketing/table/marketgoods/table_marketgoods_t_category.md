---
id: tbl_marketgoods_t_category
object_type: Table
name: 品类表 (t_category)
aliases: [t_category, marketgoods.t_category]
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

# 品类表 (t_category)

## 用途
物理表 `marketgoods.t_category`,主键 `id`。品类表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `category_code` | varchar(12) | 品类编号 |
| `category_name` | varchar(50) | 品类名称 · 可空 |
| `sup_category_code` | varchar(12) | 上级品类编号 · 可空 |
| `sup_category_name` | varchar(50) | 上级品类名称 · 可空 |
| `top_category_code` | varchar(12) | 顶级品类编号 · 可空 |
| `top_category_name` | varchar(50) | 顶级品类名称 · 可空 |
| `level` | tinyint(1) | 层级 |
| `status` | varchar(1) | 状态 1：有效 0：失效 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_category_code`:category_code (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
