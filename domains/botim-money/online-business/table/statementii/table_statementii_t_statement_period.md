---
id: tbl_statementii_t_statement_period
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
- t_statement_period
subdomain: statement
module: null
sensitivity: normal
name: 账期(t_statement_period)
aliases:
- t_statement_period
related_services:
- svc_statementii
related_scenarios: []
---
# 账期(t_statement_period)

## 用途
账期。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 账期编号 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户id |
| `statement_type` | varchar(32) | NOT NULL | 账单类型 |
| `period_type` | varchar(32) | NOT NULL | 期限类型 |
| `previous_id` | bigint |  | 上个账期id |
| `task_id` | bigint | NOT NULL | 任务id |
| `statement_id` | bigint | NOT NULL | 账单id |
| `begin_time` | timestamp | NOT NULL | 开始时间 |
| `end_time` | timestamp | NOT NULL | 结束时间 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_task_id` 唯一 (task_id)
- 索引:
  - `i_pr_bt` (begin_time)
  - `idx_merchant_mid` (merchant_mid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
