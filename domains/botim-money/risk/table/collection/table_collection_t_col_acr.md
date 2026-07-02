---
id: tbl_collection_t_col_acr
object_type: Table
name: Acr配置表 (t_col_acr)
aliases: [t_col_acr, collection.t_col_acr]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# Acr配置表 (t_col_acr)

## 用途
物理表 `collection.t_col_acr`,主键 `id`。Acr配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(50) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_by` | varchar(50) | 修改人 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `count` | int(5) | acr 值 · 可空 |
| `job_id` | bigint | 对应的账龄id · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
