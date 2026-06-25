---
id: tbl_aml_t_risk_server_switch
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
- t_risk_server_switch
subdomain: aml
module: null
sensitivity: normal
name: 风险服务开关表(t_risk_server_switch)
aliases:
- t_risk_server_switch
related_services:
- svc_aml
related_scenarios: []
---
# 风险服务开关表(t_risk_server_switch)

## 用途
风险服务开关表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL |  |
| `event_type` | varchar(32) | NOT NULL | 事件类型 |
| `risk_platform` | varchar(20) | NOT NULL | 风控平台：TMX/ALIYUN |
| `event_asyn` | tinyint(1) | NOT NULL | 事件异步：0.同步；1.异步； |
| `is_open` | tinyint(1) | NOT NULL | 是否开启；0.关闭；1.开启 |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |
| `create_by` | varchar(32) |  | 创建者 |
| `update_by` | varchar(32) |  | 更新者 |
| `remark` | varchar(64) |  | 备注 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
