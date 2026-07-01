---
id: tbl_amlrisk_leaf_alloc
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (amlrisk schema) 2026-06-25
tags:
- amlrisk
- amlrisk
- leaf_alloc
subdomain: amlrisk
module: null
sensitivity: normal
name: Sequence Config(leaf_alloc)
aliases:
- leaf_alloc
related_services:
- svc_aml
related_scenarios: []
---
# Sequence Config(leaf_alloc)

## 用途
Sequence Config。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `biz_tag` | varchar(128) | PK / NOT NULL | Sequence name |
| `max_id` | bigint | NOT NULL / 默认 1 | Max sequence id currently |
| `step` | int | NOT NULL | Cache count every time: Depends on concurrency |
| `description` | varchar(255) |  | Description |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Update time |

## 主键 / 索引
- 主键:(`biz_tag`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
