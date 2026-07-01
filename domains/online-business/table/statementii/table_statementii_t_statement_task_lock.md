---
id: tbl_statementii_t_statement_task_lock
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
- t_statement_task_lock
subdomain: statement
module: null
sensitivity: normal
name: 账单任务锁(t_statement_task_lock)
aliases:
- t_statement_task_lock
related_services:
- svc_statementii
related_scenarios: []
---
# 账单任务锁(t_statement_task_lock)

## 用途
账单任务锁。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id 主键 |
| `task_id` | bigint |  | 任务id |
| `merchant_mid` | varchar(32) |  | 商户id |
| `task_type` | varchar(32) |  | 任务类型 BALANCE 余额 TX 交易 STATEMENT 结算 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_task_mid_type` 唯一 (merchant_mid, task_type)
- 索引:
  - `idx_tl_ti` (task_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
