---
id: tbl_amlrisk_t_risk_rate_rule_item
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
- t_risk_rate_rule_item
subdomain: amlrisk
module: null
sensitivity: normal
name: risk rate rule item(t_risk_rate_rule_item)
aliases:
- t_risk_rate_rule_item
related_services:
- svc_aml
related_scenarios: []
---
# risk rate rule item(t_risk_rate_rule_item)

## 用途
risk rate rule item。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | id |
| `rule_id` | bigint | NOT NULL | rule_id |
| `criteria` | varchar(200) | NOT NULL | criteria |
| `risk_point` | int | NOT NULL | risk_point |
| `rule_exe_type` | varchar(20) | NOT NULL | rule_exe_type |
| `rules` | varchar(200) | NOT NULL | rules |
| `item_desc` | varchar(512) |  | item_desc |
| `status` | char | NOT NULL | status 1 valid 0 invalid |
| `create_time` | timestamp(3) | NOT NULL | create_time |
| `update_time` | timestamp(3) | NOT NULL | update_time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_rule_id` (rule_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
