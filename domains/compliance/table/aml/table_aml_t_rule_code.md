---
id: tbl_aml_t_rule_code
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
- t_rule_code
subdomain: aml
module: null
sensitivity: normal
name: Rule code表(t_rule_code)
aliases:
- t_rule_code
related_services:
- svc_aml
related_scenarios: []
---
# Rule code表(t_rule_code)

## 用途
Rule code表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `rule_code` | varchar(32) | PK / NOT NULL | ruleCode |
| `priority` | int(6) |  | 优先级：越小越优先 |
| `unity_result_code` | varchar(64) |  | 统一码 |

## 主键 / 索引
- 主键:(`rule_code`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
