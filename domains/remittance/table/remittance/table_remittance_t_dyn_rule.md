---
id: tbl_remittance_t_dyn_rule
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
- t_dyn_rule
subdomain: remittance
module: null
sensitivity: normal
name: Dynamic Pricing Rule(t_dyn_rule)
aliases:
- t_dyn_rule
related_services:
- svc_remittance
related_scenarios: []
---
# Dynamic Pricing Rule(t_dyn_rule)

## 用途
Dynamic Pricing Rule。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `strategy_id` | bigint | NOT NULL | Strategy ID (FK to t_dyn_strategy.id) |
| `rule_index` | int | NOT NULL / 默认 0 | Execution order of the rule |
| `rule_name` | varchar(64) | NOT NULL | Rule Name |
| `logic_group` | int | NOT NULL / 默认 0 | Logic group ID (same group rules are combined) |
| `logic_operator` | varchar(8) | NOT NULL / 默认 'AND' | Logic operator within group: AND/OR |
| `condition_js` | varchar(512) | NOT NULL | Condition definition in JSON DSL |
| `enabled` | char | NOT NULL / 默认 'Y' | Enabled Flag (Y/N) |
| `gmt_create` | timestamp | NOT NULL | Creation timestamp |
| `gmt_modified` | timestamp | NOT NULL | Last modification timestamp |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_strategy_index` (strategy_id, rule_index)
  - `idx_strategy_logic` (strategy_id, logic_group)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
