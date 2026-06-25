---
id: tbl_amlrisk_t_personal_decision_log
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
- t_personal_decision_log
subdomain: amlrisk
module: null
sensitivity: normal
name: 个人扫描决策日志(t_personal_decision_log)
aliases:
- t_personal_decision_log
related_services:
- svc_aml
related_scenarios: []
---
# 个人扫描决策日志(t_personal_decision_log)

## 用途
个人扫描决策日志。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `personal_id` | bigint |  | 个人信息表id |
| `result_id` | bigint |  | 个人扫描结果id |
| `decision` | varchar(100) |  | 决策 |
| `comment` | varchar(500) |  | 备注 |
| `operator` | varchar(50) |  | 操作人 |
| `CREATED_TIME` | timestamp |  | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
