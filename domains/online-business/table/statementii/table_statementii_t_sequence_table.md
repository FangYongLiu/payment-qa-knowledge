---
id: tbl_statementii_t_sequence_table
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (statementii schema) 2026-06-25
tags:
- statementii
- statement
- t_sequence_table
subdomain: statement
module: null
sensitivity: normal
name: 序号生成表(t_sequence_table)
aliases:
- t_sequence_table
related_services:
- svc_statementii
related_scenarios: []
---
# 序号生成表(t_sequence_table)

## 用途
序号生成表。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
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
