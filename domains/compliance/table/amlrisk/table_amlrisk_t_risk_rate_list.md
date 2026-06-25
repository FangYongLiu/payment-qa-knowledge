---
id: tbl_amlrisk_t_risk_rate_list
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
- t_risk_rate_list
subdomain: amlrisk
module: null
sensitivity: normal
name: risk rate list(t_risk_rate_list)
aliases:
- t_risk_rate_list
related_services:
- svc_aml
related_scenarios: []
---
# risk rate list(t_risk_rate_list)

## 用途
risk rate list。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `list_library` | varchar(50) | NOT NULL | list_library |
| `list_value` | varchar(200) | NOT NULL | list_value |
| `status` | char | NOT NULL | status 1 valid 0 invalid |
| `list_type` | varchar(20) | NOT NULL | list_type FUZZY_MATCH REGEX_MATCH COMPLETE_MATCH |
| `create_time` | timestamp(3) | NOT NULL | create_time |
| `update_time` | timestamp(3) | NOT NULL | update_time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_list_library` (list_library)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
