---
id: tbl_statementii_t_template_version_change_log
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (statementii schema) 2026-06-25
tags:
- statementii
- statement
- t_template_version_change_log
subdomain: statement
module: null
sensitivity: normal
name: template version change log(t_template_version_change_log)
aliases:
- t_template_version_change_log
related_services:
- svc_statementii
related_scenarios: []
---
# template version change log(t_template_version_change_log)

## 用途
template version change log。属 statementii 库,由 [[svc_statementii]] 读写。

## 关联关系
- **所属服务**:[[svc_statementii]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id 主键 |
| `merchant_mid` | varchar(32) | NOT NULL | merchant mid |
| `statement_type` | varchar(32) | NOT NULL | statement type |
| `previous_version` | varchar(32) | NOT NULL | previous version |
| `current_version` | varchar(32) | NOT NULL | current version |
| `update_by` | varchar(32) |  | updateBy |
| `created_time` | timestamp | NOT NULL | created_time |
| `period_type` | varchar(32) | NOT NULL | period_type |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `i_tvcl_ct` (created_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
