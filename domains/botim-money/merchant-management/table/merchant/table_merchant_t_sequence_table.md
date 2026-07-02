---
id: tbl_merchant_t_sequence_table
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_sequence_table
subdomain: merchant
module: null
sensitivity: normal
name: 序号生成表(t_sequence_table)
aliases:
- t_sequence_table
related_services:
- svc_merchant
related_scenarios: []
---
# 序号生成表(t_sequence_table)

## 用途
序号生成表。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `sequence_name` | varchar(128) | PK / NOT NULL | 序列名称 |
| `sequence_value` | bigint |  | 序列值 |

## 主键 / 索引
- 主键:(`sequence_name`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
