---
id: tbl_statementii_t_statement_rebate
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
- t_statement_rebate
subdomain: statement
module: null
sensitivity: normal
name: rebate statement(t_statement_rebate)
aliases:
- t_statement_rebate
related_services:
- svc_statementii
related_scenarios: []
---
# rebate statement(t_statement_rebate)

## 用途
rebate statement。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id  |
| `merchant_mid` | varchar(50) | NOT NULL | merchant id |
| `task_id` | bigint | NOT NULL | task id |
| `file_path` | varchar(200) | NOT NULL | file path |
| `records` | int |  | record number |
| `currency_code` | varchar(20) | NOT NULL | currency |
| `total_credit` | decimal(19,4) | NOT NULL | total income |
| `total_debit` | decimal(19,4) | NOT NULL | total outcome |
| `total_credit_rebate` | decimal(19,4) | NOT NULL | total rebate income |
| `total_debit_rebate` | decimal(19,4) | NOT NULL | total rebate outcome |
| `invoice_file_path` | varchar(200) |  | invoice path |
| `params` | varchar(500) |  | extension param |
| `invoice_id` | bigint |  | invoice id |
| `xlsx_file_path` | varchar(200) |  | xlsx path |
| `pdf_file_path` | varchar(200) |  | pdf path |
| `created_time` | timestamp | NOT NULL | create time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UIDX_TASK_ID` 唯一 (task_id)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
