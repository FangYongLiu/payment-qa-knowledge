---
id: tbl_remittance_t_dyn_cohort_config
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
- t_dyn_cohort_config
subdomain: remittance
module: null
sensitivity: normal
name: Cohort Configuration Table(t_dyn_cohort_config)
aliases:
- t_dyn_cohort_config
related_services:
- svc_remittance
related_scenarios: []
---
# Cohort Configuration Table(t_dyn_cohort_config)

## 用途
Cohort Configuration Table。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `name` | varchar(64) | NOT NULL | Cohort Name |
| `id_type` | varchar(20) | NOT NULL | Identifier type: MEMBER_ID, MOBILE_NO |
| `description` | varchar(255) |  | Cohort Description |
| `source` | varchar(20) | NOT NULL / 默认 'SYSTEM' | Source: SYSTEM, UPLOAD |
| `match_mode` | varchar(10) | NOT NULL / 默认 'ANY' | Rule match mode: ANY(OR logic)/ALL(AND logic) |
| `status` | varchar(20) | NOT NULL / 默认 'ACTIVE' | Status: ACTIVE, INACTIVE |
| `created_by` | varchar(64) |  | Creator |
| `modified_by` | varchar(64) |  | Last modifier |
| `gmt_create` | timestamp | NOT NULL | Creation timestamp |
| `gmt_modified` | timestamp | NOT NULL | Last modification timestamp |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_cohort_name` 唯一 (name)
- 索引:
  - `idx_created_by` (created_by)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
