---
id: tbl_remittance_t_dyn_strategy
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
- t_dyn_strategy
subdomain: remittance
module: null
sensitivity: normal
name: Dynamic Pricing Strategy - Simplified Without Version History(t_dyn_strategy)
aliases:
- t_dyn_strategy
related_services:
- svc_remittance
related_scenarios: []
---
# Dynamic Pricing Strategy - Simplified Without Version History(t_dyn_strategy)

## 用途
Dynamic Pricing Strategy - Simplified Without Version History。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `strategy_code` | varchar(32) | NOT NULL | Strategy Code (business identifier) |
| `name` | varchar(64) | NOT NULL | Strategy Name |
| `event_code` | varchar(20) | NOT NULL | Triggering event code (PRE_QUOTE/POST_QUOTE/etc) |
| `priority` | int | NOT NULL / 默认 0 | Priority (higher value means higher priority) |
| `match_mode` | varchar(10) | NOT NULL / 默认 'ANY' | rule match mode, (ANY/ALL) |
| `effect_start` | datetime |  | Effective start time |
| `effect_end` | datetime |  | Effective end time |
| `status` | varchar(20) | NOT NULL / 默认 'Upcoming' | Status: Upcoming/Paused/Running/Finished |
| `action_type` | varchar(32) | NOT NULL | Action Type when strategy matches |
| `action_js` | varchar(512) | NOT NULL | Action parameters in JSON (supports multiple actions) |
| `enabled` | char | NOT NULL / 默认 'Y' | Enabled Flag (Y/N) |
| `memo` | varchar(255) |  | Strategy Description |
| `created_by` | varchar(64) |  | Strategy creator |
| `modified_by` | varchar(64) |  | Last modifier |
| `gmt_create` | timestamp | NOT NULL | Creation timestamp |
| `gmt_modified` | timestamp | NOT NULL | Last modification timestamp |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_strategy_event_priority` 唯一 (strategy_code, event_code, priority)
- 索引:
  - `idx_created_by` (created_by)
  - `idx_event_priority` (event_code, priority)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
