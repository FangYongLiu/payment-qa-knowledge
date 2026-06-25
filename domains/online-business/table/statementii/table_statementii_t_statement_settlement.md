---
id: tbl_statementii_t_statement_settlement
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
- t_statement_settlement
subdomain: statement
module: null
sensitivity: normal
name: 结算对账单(t_statement_settlement)
aliases:
- t_statement_settlement
related_services:
- svc_statementii
related_scenarios: []
---
# 结算对账单(t_statement_settlement)

## 用途
结算对账单。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id 主键 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户id |
| `task_id` | bigint | NOT NULL | 任务id |
| `file_path` | varchar(200) | NOT NULL | 文件路径 |
| `records` | int |  | 记录数 |
| `total_credit` | decimal(19,4) | NOT NULL | 总收入 |
| `total_debit` | decimal(19,4) | NOT NULL | 总支出 |
| `begin_balance` | decimal(19,4) | NOT NULL | 期初余额 |
| `ending_balance` | decimal(19,4) | NOT NULL | 期末余额 |
| `reserved_amount` | decimal(19,4) | NOT NULL | 预留金额 |
| `min_withdraw_amount` | decimal(19,4) |  | 最小提现金额 |
| `withdrawable_amount` | decimal(19,4) | NOT NULL | 可提现金额 |
| `stay_amount` | decimal(19,4) | NOT NULL | 滞留金额 |
| `settlement_amount` | decimal(19,4) | NOT NULL | 结算金额 |
| `currency_code` | varchar(20) | NOT NULL | 币种 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `xlsx_file_path` | varchar(200) |  | xlsx 文件路径 |
| `pdf_file_path` | varchar(200) |  | pdf 文件路径 |
| `total_comm` | decimal(19,4) |  | 税前金额 |
| `total_vat` | decimal(19,4) |  | 税额 |
| `total_comm_vat` | decimal(19,4) |  | 税前金额加税额 |
| `invoice_file_path` | varchar(200) |  | 发票路径 |
| `params` | varchar(500) |  | 扩展参数 |
| `invoice_id` | bigint |  | 发票ID |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UIDX_TASK_ID` 唯一 (task_id)
- 索引:
  - `idx_task_id` (task_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
