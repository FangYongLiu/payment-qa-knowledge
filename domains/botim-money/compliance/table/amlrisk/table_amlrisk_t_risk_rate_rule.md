---
id: tbl_amlrisk_t_risk_rate_rule
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
- t_risk_rate_rule
subdomain: amlrisk
module: null
sensitivity: normal
name: risk rate rule(t_risk_rate_rule)
aliases:
- t_risk_rate_rule
related_services:
- svc_aml
related_scenarios: []
---
# risk rate rule(t_risk_rate_rule)

## 用途
risk rate rule。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | id |
| `rule_type` | varchar(20) | NOT NULL | rule_type(PERSONAL/MERCHANT) |
| `rule_title` | varchar(100) | NOT NULL | rule_title |
| `max_risk_point` | int | NOT NULL | max_risk_point |
| `rule_desc` | varchar(512) |  | rule_desc |
| `weight` | decimal(19,4) | NOT NULL | weight |
| `status` | char | NOT NULL | status 1 valid 0 invalid |
| `create_time` | timestamp(3) | NOT NULL | create_time |
| `update_time` | timestamp(3) | NOT NULL | update_time |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
