---
id: tbl_aml_t_fraudpool_operation
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_fraudpool_operation
subdomain: aml
module: null
sensitivity: normal
name: log t_fraud_pool operation(t_fraudpool_operation)
aliases:
- t_fraudpool_operation
related_services:
- svc_aml
related_scenarios: []
---
# log t_fraud_pool operation(t_fraudpool_operation)

## 用途
log t_fraud_pool operation。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `fraud_pool_id` | bigint | NOT NULL | key of t_fraud_pool |
| `operation_type` | varchar(16) |  | operator_type |
| `operation_content` | varchar(1024) |  | previous version of the record |
| `operator` | varchar(32) |  | operator |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | update_time |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | create time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_fraudpool_id` (fraud_pool_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
