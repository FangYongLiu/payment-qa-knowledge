---
id: tbl_aml_t_chargeback_operator
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
- t_chargeback_operator
subdomain: aml
module: null
sensitivity: normal
name: chargeback operator(t_chargeback_operator)
aliases:
- t_chargeback_operator
related_services:
- svc_aml
related_scenarios: []
---
# chargeback operator(t_chargeback_operator)

## 用途
chargeback operator。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `chargeback_id` | bigint |  | chargeback_id |
| `operator_type` | varchar(32) | NOT NULL | operator_type |
| `operator_time` | timestamp(3) | NOT NULL | operator_time |
| `operator_content` | varchar(128) | NOT NULL | operator_content |
| `operator` | varchar(32) | NOT NULL | operator |
| `create_time` | timestamp(3) | 默认 CURRENT_TIMESTAMP(3) | createTime |
| `update_time` | timestamp(3) | 默认 CURRENT_TIMESTAMP(3) | updateTime |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_chargeback_id` (chargeback_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
