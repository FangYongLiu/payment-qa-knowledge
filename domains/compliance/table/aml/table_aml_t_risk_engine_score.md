---
id: tbl_aml_t_risk_engine_score
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
- t_risk_engine_score
subdomain: aml
module: null
sensitivity: normal
name: 风控引擎默认风险值表(t_risk_engine_score)
aliases:
- t_risk_engine_score
related_services:
- svc_aml
related_scenarios: []
---
# 风控引擎默认风险值表(t_risk_engine_score)

## 用途
风控引擎默认风险值表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL |  |
| `risk_platform` | varchar(20) |  | 风控平台：TMX/ALIYUN |
| `risk_engine` | varchar(20) |  | 风控引擎：AML/FRAUD |
| `default_score` | int |  | 默认风险值 |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |
| `create_by` | varchar(32) |  | 创建者 |
| `update_by` | varchar(32) |  | 更新者 |
| `event_specific` | varchar(32) |  | 具体的事件类型 |
| `remark` | varchar(64) |  | 备注 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
