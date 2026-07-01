---
id: tbl_remittance_t_dyn_strategy_cohort_mapping
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
- t_dyn_strategy_cohort_mapping
subdomain: remittance
module: null
sensitivity: normal
name: Strategy to Cohort Configuration Mapping Table(t_dyn_strategy_cohort_mapping)
aliases:
- t_dyn_strategy_cohort_mapping
related_services:
- svc_remittance
related_scenarios: []
---
# Strategy to Cohort Configuration Mapping Table(t_dyn_strategy_cohort_mapping)

## 用途
Strategy to Cohort Configuration Mapping Table。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `strategy_id` | bigint | NOT NULL | Strategy ID (FK to t_dyn_strategy.id) |
| `cohort_config_id` | bigint | NOT NULL | Cohort Config ID (FK to t_dyn_cohort_config.id) |
| `gmt_create` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Creation timestamp |
| `gmt_modified` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | Last modification timestamp |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_strategy_cohort` 唯一 (strategy_id, cohort_config_id)
- 索引:
  - `idx_cohort_config_id` (cohort_config_id)
  - `idx_strategy_id` (strategy_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
