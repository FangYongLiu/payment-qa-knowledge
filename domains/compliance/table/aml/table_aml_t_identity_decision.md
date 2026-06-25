---
id: tbl_aml_t_identity_decision
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
- t_identity_decision
subdomain: aml
module: null
sensitivity: normal
name: 核身决策表(t_identity_decision)
aliases:
- t_identity_decision
related_services:
- svc_aml
related_scenarios: []
---
# 核身决策表(t_identity_decision)

## 用途
核身决策表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `tid` | varchar(72) |  | tid |
| `rule_id` | bigint | 默认 0 | 命中的规则ID |
| `event_type` | varchar(50) | NOT NULL | 事件类型 |
| `cis_salt` | varbinary(100) | NOT NULL | 加密盐值 |
| `cis_ticket` | varchar(100) | NOT NULL | 系统生成唯一票据,校验结果时用 |
| `identity_type` | varchar(255) | 默认 '' | 核身方式 |
| `is_over` | tinyint(2) | 默认 0 | 是否完成-0.未完成;1.已完成; |
| `risk_score` | smallint | 默认 0 | 风险分值 |
| `decision_factor` | varchar(512) |  | 决策因子 |
| `failure_times` | smallint | 默认 0 | 失败次数 |
| `member_id` | varchar(32) | 默认 '' | 会员ID |
| `global_biz_id` | varchar(32) | 默认 '' | 全局业务ID |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |
| `remarks` | varchar(50) | 默认 '' | 备注说明 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `cis_ticket` (cis_ticket)
  - `create_time` (create_time)
  - `global_biz_id` (global_biz_id)
  - `member_id` (member_id)
  - `tid` (tid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
