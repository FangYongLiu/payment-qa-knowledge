---
id: tbl_pcbs_t_aggregation_auxiliary
object_type: Table
name: Aggregation Auxiliary (t_aggregation_auxiliary)
aliases: [t_aggregation_auxiliary, pcbs.t_aggregation_auxiliary]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcbs schema DDL
tags: [settlement, pcbs]
sensitivity: normal
related_services: []
---

# Aggregation Auxiliary (t_aggregation_auxiliary)

## 用途
物理表 `pcbs.t_aggregation_auxiliary`,主键 `id`。Aggregation Auxiliary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID · 可空 |
| `code` | varchar(32) | Code · 可空 |
| `data_value` | varchar(100) | Value · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
