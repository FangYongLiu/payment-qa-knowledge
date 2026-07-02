---
id: tbl_statementii_t_statement_transaction
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
- t_statement_transaction
subdomain: statement
module: null
sensitivity: normal
name: 交易对账单(t_statement_transaction)
aliases:
- t_statement_transaction
related_services:
- svc_statementii
related_scenarios: []
---
# 交易对账单(t_statement_transaction)

## 用途
交易对账单。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id 主键 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户id |
| `task_id` | bigint | NOT NULL | 任务id |
| `file_path` | varchar(200) | NOT NULL | 文件路径 |
| `records` | int |  | 记录数 |
| `purchase_nums` | int | NOT NULL | 总收单笔数 |
| `purchase_amount` | decimal(19,4) | NOT NULL | 总收单金额 |
| `refund_nums` | int | NOT NULL | 总退款笔数 |
| `refund_amount` | decimal(19,4) | NOT NULL | 总退款金额 |
| `currency_code` | varchar(20) | NOT NULL | 币种 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `xlsx_file_path` | varchar(200) |  | xlsx 文件路径 |
| `pdf_file_path` | varchar(200) |  | pdf 文件路径 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UIDX_TASK_ID` 唯一 (task_id)
- 索引:
  - `idx_merchant_mid` (merchant_mid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
