---
id: tbl_aml_t_status_score_testrun_result
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
- t_status_score_testrun_result
subdomain: aml
module: null
sensitivity: normal
name: 状态分数试运行结果(t_status_score_testrun_result)
aliases:
- t_status_score_testrun_result
related_services:
- svc_aml
related_scenarios: []
---
# 状态分数试运行结果(t_status_score_testrun_result)

## 用途
状态分数试运行结果。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `tid` | varchar(32) | 默认 '' | 业务跟踪ID |
| `status_score_id` | bigint | 默认 0 | 状态分数配置ID |
| `event_type` | varchar(50) |  | 事件类型 |
| `risk_score` | int |  | 风险分值 |
| `risk_result` | varchar(10) |  | 风控结果 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `create_time_index` (create_time)
  - `tid_index` (tid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
