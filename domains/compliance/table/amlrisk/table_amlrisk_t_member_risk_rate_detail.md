---
id: tbl_amlrisk_t_member_risk_rate_detail
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
- t_member_risk_rate_detail
subdomain: amlrisk
module: null
sensitivity: normal
name: member risk rate detail(t_member_risk_rate_detail)
aliases:
- t_member_risk_rate_detail
related_services:
- svc_aml
related_scenarios: []
---
# member risk rate detail(t_member_risk_rate_detail)

## 用途
member risk rate detail。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `rate_id` | bigint | NOT NULL | rate_id |
| `rule_id` | bigint | NOT NULL | rule_id |
| `rule_item_id` | bigint | NOT NULL | rule_item_id |
| `risk_point` | int | NOT NULL | risk_point |
| `risk_score` | decimal(19,4) | NOT NULL | risk_score |
| `create_time` | timestamp(3) | NOT NULL | create_time |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_rate_id` (rate_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
