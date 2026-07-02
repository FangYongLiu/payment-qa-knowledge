---
id: tbl_aml_t_identity_rule_testrun_result
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
- t_identity_rule_testrun_result
subdomain: aml
module: null
sensitivity: normal
name: 核身规则试运行结果(t_identity_rule_testrun_result)
aliases:
- t_identity_rule_testrun_result
related_services:
- svc_aml
related_scenarios: []
---
# 核身规则试运行结果(t_identity_rule_testrun_result)

## 用途
核身规则试运行结果。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `tid` | varchar(32) | 默认 '' | 业务跟踪ID |
| `rule_id` | bigint | 默认 0 | 命中的规则ID |
| `event_type` | varchar(50) |  | 事件类型 |
| `risk_score` | int |  | 风险分值 |
| `identity_type` | varchar(255) |  | 核身方式 |
| `global_biz_id` | varchar(32) |  | 全局业务ID |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `create_time_index` (create_time)
  - `rule_id_index` (rule_id)
  - `tid_index` (tid)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
