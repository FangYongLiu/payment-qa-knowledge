---
id: tbl_aml_t_freeze_task
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
- t_freeze_task
subdomain: aml
module: null
sensitivity: normal
name: freeze task(t_freeze_task)
aliases:
- t_freeze_task
related_services:
- svc_aml
related_scenarios: []
---
# freeze task(t_freeze_task)

## 用途
freeze task。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `task_no` | bigint | PK / NOT NULL | task no |
| `member_id` | varchar(20) | NOT NULL | member id |
| `account_no` | varchar(30) | NOT NULL | account no |
| `freeze_amount` | decimal(19,4) | NOT NULL | need freeze amount |
| `frozen_amount` | decimal(19,4) | NOT NULL | frozen amount |
| `currency` | char(3) | NOT NULL | currency |
| `status` | varchar(10) | NOT NULL | status：I P S |
| `extension` | varchar(255) |  | extension |
| `memo` | varchar(255) |  | memo |
| `operator` | varchar(30) | NOT NULL | operator |
| `create_time` | timestamp(3) | NOT NULL | create time |
| `update_time` | timestamp(3) | NOT NULL | update time |
| `client_id` | varchar(30) | NOT NULL | client id |

## 主键 / 索引
- 主键:(`task_no`)
- 索引:
  - `idx_freeze_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
