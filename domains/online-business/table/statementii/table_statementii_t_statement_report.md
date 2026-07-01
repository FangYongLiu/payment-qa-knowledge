---
id: tbl_statementii_t_statement_report
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
- t_statement_report
subdomain: statement
module: null
sensitivity: normal
name: 对账单报表(t_statement_report)
aliases:
- t_statement_report
related_services:
- svc_statementii
related_scenarios: []
---
# 对账单报表(t_statement_report)

## 用途
对账单报表。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id 主键 |
| `report_file_path` | varchar(200) | NOT NULL | report file path |
| `begin_time` | timestamp | NOT NULL | 开始时间 |
| `end_time` | timestamp | NOT NULL | 结束时间 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
