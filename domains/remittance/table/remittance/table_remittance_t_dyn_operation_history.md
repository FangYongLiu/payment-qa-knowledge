---
id: tbl_remittance_t_dyn_operation_history
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
- t_dyn_operation_history
subdomain: remittance
module: null
sensitivity: normal
name: Operation History Table - Tracks all user and system operations(t_dyn_operation_history)
aliases:
- t_dyn_operation_history
related_services:
- svc_remittance
related_scenarios: []
---
# Operation History Table - Tracks all user and system operations(t_dyn_operation_history)

## 用途
Operation History Table - Tracks all user and system operations。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `operation_type` | varchar(32) | NOT NULL | Operation Type: CREATE/UPDATE/DELETE/PAUSE/RESUME/ACTIVATE/DEACTIVATE/PRIORITY_CHANGE/BATCH_UPLOAD/etc |
| `entity_type` | varchar(32) | NOT NULL | Target Entity Type: STRATEGY/COHORT_CONFIG/COHORT/RULE/COHORT_RULE |
| `entity_id` | bigint | NOT NULL | Target Entity ID |
| `entity_name` | varchar(64) |  | Target Entity Name (for display) |
| `operator_type` | varchar(16) | NOT NULL / 默认 'USER' | Operator Type: USER/SYSTEM |
| `operator_id` | varchar(64) |  | Operator ID (user account or system identifier) |
| `operator_name` | varchar(64) |  | Operator Display Name |
| `operation_desc` | varchar(255) | NOT NULL | Operation Description (user-friendly) |
| `operation_reason` | varchar(255) |  | Operation Reason/Comment |
| `before_value` | text |  | Before value snapshot (JSON format) |
| `after_value` | text |  | After value snapshot (JSON format) |
| `operation_context` | text |  | Operation context data (JSON format) |
| `trigger_condition` | varchar(64) |  | System operation trigger condition (budget_limit/time_expired/etc) |
| `auto_action` | char | NOT NULL / 默认 'N' | Is automatic action (Y/N) |
| `client_ip` | varchar(45) |  | Client IP Address |
| `user_agent` | varchar(255) |  | User Agent |
| `request_id` | varchar(64) |  | Request ID for tracing |
| `session_id` | varchar(64) |  | Session ID |
| `gmt_create` | timestamp | NOT NULL | Operation timestamp |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_entity` (entity_type, entity_id)
  - `idx_entity_time` (entity_type, entity_id, gmt_create)
  - `idx_gmt_create` (gmt_create)
  - `idx_operator` (operator_type, operator_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
