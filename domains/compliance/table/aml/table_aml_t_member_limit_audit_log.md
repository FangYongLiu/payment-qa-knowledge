---
id: tbl_aml_t_member_limit_audit_log
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
- t_member_limit_audit_log
subdomain: aml
module: null
sensitivity: normal
name: Limit Audit Log(t_member_limit_audit_log)
aliases:
- t_member_limit_audit_log
related_services:
- svc_aml
related_scenarios: []
---
# Limit Audit Log(t_member_limit_audit_log)

## 用途
Limit Audit Log。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id |
| `apply_id` | int | NOT NULL | apply id |
| `operator` | varchar(20) |  | Operator |
| `role` | varchar(20) |  | Role: System,Risk,Compliance |
| `audit_status` | varchar(20) |  | Audit Status:New Reupload Pass Reject |
| `remarks` | varchar(255) |  | Remarks |
| `create_time` | timestamp(3) |  | Create Time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_apply_id` (apply_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
