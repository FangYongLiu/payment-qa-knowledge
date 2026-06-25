---
id: tbl_statement_db
object_type: Table
name: 账单库 statementii 核心表(statementii)
aliases:
- statementii
- 账单库
related_scenarios: []
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 账单
- 对账单
- 账期
related_services: []
related_tables:
- tbl_merchant_db
- tbl_statementii_t_retry_task
- tbl_statementii_t_sequence_table
- tbl_statementii_t_settlement_config
- tbl_statementii_t_settlement_config_bak
- tbl_statementii_t_settlement_order
- tbl_statementii_t_statement_balance
- tbl_statementii_t_statement_config
- tbl_statementii_t_statement_period
- tbl_statementii_t_statement_rebate
- tbl_statementii_t_statement_report
- tbl_statementii_t_statement_settlement
- tbl_statementii_t_statement_subscribe
- tbl_statementii_t_statement_task
- tbl_statementii_t_statement_task_lock
- tbl_statementii_t_statement_transaction
- tbl_statementii_t_template_version_change_log
- tbl_trade_db
---

# 账单库 statementii 核心表(statementii)

## 用途
账单库 `statementii` 用于管理账期、对账单登记/模板/任务/文件,以及收单对账单的统计信息,支撑商户对账单生成与下发流程。

> 这是 `statementii` 库的**库级速查对象**(多张表的清单),字段级明细以各表为准;尚无单表独立对象的字段标「待补」。

## 关联关系
- **所属服务**:待补(payment-core 域内暂无对账单/账单服务对象,不硬连)。
- **谁读写它**:收单对账统计来源于交易数据 [[tbl_trade_db]];商户维度联查 [[tbl_merchant_db]]。
- **哪些场景校验它**:待补(尚无 `related_scenarios`)。
- 导航入口见 [[ts_payment_db_navigation]]。

## 关键列
| 表 | 说明 |
| --- | --- |
| `t_statement_period` | 账期表,定义对账单的账期周期 |
| `t_statement_registration` | 对账单登记表,记录对账单订阅/登记关系 |
| `t_statement_template` | 对账单模板,定义对账单的格式与字段配置 |
| `t_statement_task` | 对账单任务,账单生成的任务调度记录 |
| `t_statement_file` | 对账单文件,存放生成后的对账单文件信息 |
| `t_statement_pruchase_statistics` | 收单对账单信息统计表(注意原文表名拼写为 `pruchase`) |

各表物理字段定义:待补(原文未提供)。

## 主键 / 索引
待补:原文未提供。

## 校验点(QA 关注)
- 账期 `t_statement_period` 与登记 `t_statement_registration`、任务 `t_statement_task` 之间的关联是否一致。
- 对账单模板 `t_statement_template` 与任务、文件的对应关系是否正确生成。
- `t_statement_file` 文件记录与实际生成文件是否匹配;任务状态是否正确流转。
- `t_statement_pruchase_statistics` 收单统计数据与 [[tbl_trade_db]] 收单交易数据是否一致。
- 注意表名 `t_statement_pruchase_statistics` 的拼写(原文如此),SQL 编写时不要误改为 `purchase`。
