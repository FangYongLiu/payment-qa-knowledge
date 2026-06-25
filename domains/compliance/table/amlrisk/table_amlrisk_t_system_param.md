---
id: tbl_amlrisk_t_system_param
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (amlrisk schema) 2026-06-25
tags:
- amlrisk
- amlrisk
- t_system_param
subdomain: amlrisk
module: null
sensitivity: normal
name: 营销系统通用设置(t_system_param)
aliases:
- t_system_param
related_services:
- svc_aml
related_scenarios: []
---
# 营销系统通用设置(t_system_param)

## 用途
营销系统通用设置。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键ID |
| `param_type` | varchar(32) | NOT NULL | 参数类型 |
| `param_key` | varchar(64) | NOT NULL | 参数key |
| `param_value` | varchar(255) | NOT NULL | 参数value |
| `status` | varchar(16) | NOT NULL | 状态 |
| `created_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UK_COMMON_SETTING` 唯一 (param_type, param_key)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
