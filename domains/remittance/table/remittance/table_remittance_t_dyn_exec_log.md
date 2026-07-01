---
id: tbl_remittance_t_dyn_exec_log
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_dyn_exec_log
subdomain: remittance
module: null
sensitivity: normal
name: Dynamic Pricing Execution Log(t_dyn_exec_log)
aliases:
- t_dyn_exec_log
related_services:
- svc_remittance
related_scenarios: []
---
# Dynamic Pricing Execution Log(t_dyn_exec_log)

## 用途
Dynamic Pricing Execution Log。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `order_no` | bigint |  | Order Number |
| `member_id` | varchar(20) |  | Member ID |
| `event_code` | varchar(32) | NOT NULL | Event Code |
| `send_amount` | —(DDL未定义) |  |  |
| `receive_country` | —(DDL未定义) |  |  |
| `channel_code` | —(DDL未定义) |  |  |
| `mobile_no` | varchar(32) |  | mobile phone no |
| `strategy_id` | bigint | NOT NULL | Strategy ID |
| `rule_ids` | varchar(255) |  | Applied Rule IDs (comma separated) |
| `execution_result` | varchar(32) | NOT NULL / 默认 'SUCCESS' | Execution Result: SUCCESS/FAILED/SKIPPED |
| `skip_reason` | varchar(128) |  | Skip Reason (time_expired/usage_limit/user_limit) |
| `latency_ms` | int | NOT NULL | Execution latency in milliseconds |
| `result_js` | varchar(512) |  | Result snapshot in JSON |
| `gmt_create` | timestamp | NOT NULL | Creation timestamp |
| `matched` | char | NOT NULL / 默认 'N' | Matched Flag (Y/N) |
| `new_user` | —(DDL未定义) |  |  |
| `gmt_update` | —(DDL未定义) |  |  |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_event_time` (event_code, gmt_create)
  - `idx_gmt` (gmt_create)
  - `idx_member_time` (member_id, gmt_create)
  - `idx_order` (order_no)
  - `idx_strategy_id` (strategy_id)
  - `idx_strategy_result` (mobile_no, execution_result)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
