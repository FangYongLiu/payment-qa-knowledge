---
id: tbl_remittance_t_dyn_cohort
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
- t_dyn_cohort
subdomain: remittance
module: null
sensitivity: normal
name: Cohort Data Table(t_dyn_cohort)
aliases:
- t_dyn_cohort
related_services:
- svc_remittance
related_scenarios: []
---
# Cohort Data Table(t_dyn_cohort)

## 用途
Cohort Data Table。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary Key |
| `cohort_config_id` | bigint | NOT NULL | Cohort Config ID (FK to t_dyn_cohort_config.id) |
| `id_value` | varchar(32) | NOT NULL | Identifier value (member_id or mobile_no) |
| `status` | varchar(20) | NOT NULL / 默认 'ACTIVE' | Status: ACTIVE, INACTIVE |
| `batch_no` | varchar(32) |  | Batch number for upload tracking |
| `gmt_create` | timestamp | NOT NULL | Creation timestamp |
| `gmt_modified` | timestamp | NOT NULL | Last modification timestamp |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_cohort_config_id_value` 唯一 (cohort_config_id, id_value)
- 索引:
  - `idx_cohort_config_id` (cohort_config_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
