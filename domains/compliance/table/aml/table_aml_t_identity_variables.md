---
id: tbl_aml_t_identity_variables
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
- t_identity_variables
subdomain: aml
module: null
sensitivity: normal
name: 核身变量表(t_identity_variables)
aliases:
- t_identity_variables
related_services:
- svc_aml
related_scenarios: []
---
# 核身变量表(t_identity_variables)

## 用途
核身变量表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `variable_name` | varchar(128) | NOT NULL | 变量名称 |
| `variable_type` | varchar(32) | NOT NULL | 变量类型：countDistinct、velocity |
| `identity_type` | varchar(100) |  | 核身方式 |
| `check_result` | char |  | 验证结果；F：失败；S.成功； |
| `rule_condition` | varchar(1000) |  | 规则条件 |
| `times` | int |  | 时长 |
| `times_unit` | varchar(10) |  | 时长单位 |
| `dimensions` | varchar(255) |  | 维度 |
| `report_col` | varchar(32) |  | 变量统计的字段（类如金额字段） |
| `status` | char |  | 状态 1有效 0无效 |
| `memo` | varchar(128) |  | 备注 |
| `create_time` | timestamp |  | 创建时间 |
| `create_by` | varchar(32) |  | 创建人 |
| `update_time` | timestamp |  | 更新时间 |
| `update_by` | varchar(32) |  | 更新人 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `variable_name_index` 唯一 (variable_name)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
