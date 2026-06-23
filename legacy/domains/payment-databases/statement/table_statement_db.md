---
id: tbl_statement_db
object_type: Table
domain: payment-database-reference
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 账单
- 对账单
- 账期
subdomain: statement
module: null
sensitivity: normal
name: 账单库(statementii)核心表
aliases:
- statementii
related_services: []
related_tables:
- tbl_merchant_db
- tbl_trade_db
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
账单库 `statementii` 用于管理账期、对账单登记/模板/任务/文件，以及收单对账单的统计信息，支撑商户对账单生成与下发流程。

## 关键列
- `statementii.t_statement_period`：账期表，定义对账单的账期周期。
- `statementii.t_statement_registration`：对账单登记表，记录对账单订阅/登记关系。
- `statementii.t_statement_template`：对账单模板，定义对账单的格式与字段配置。
- `statementii.t_statement_task`：对账单任务，账单生成的任务调度记录。
- `statementii.t_statement_file`：对账单文件，存放生成后的对账单文件信息。
- `statementii.t_statement_pruchase_statistics`：收单对账单信息统计表（注意原文表名拼写为 `pruchase`）。

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 账期 `t_statement_period` 与登记 `t_statement_registration`、任务 `t_statement_task` 之间的关联是否一致。
- 对账单模板 `t_statement_template` 与任务、文件的对应关系是否正确生成。
- `t_statement_file` 文件记录与实际生成文件是否匹配；任务状态是否正确流转。
- `t_statement_pruchase_statistics` 收单统计数据与 [[tbl_trade_db]] 收单交易数据是否一致。
- 注意表名 `t_statement_pruchase_statistics` 的拼写（原文如此），SQL 编写时不要误改为 `purchase`。
