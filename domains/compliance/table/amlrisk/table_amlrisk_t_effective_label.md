---
id: tbl_amlrisk_t_effective_label
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
- t_effective_label
subdomain: amlrisk
module: null
sensitivity: normal
name: effective label(t_effective_label)
aliases:
- t_effective_label
related_services:
- svc_aml
related_scenarios: []
---
# effective label(t_effective_label)

## 用途
effective label。属 amlrisk 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | id |
| `member_id` | varchar(20) | NOT NULL | member_id |
| `risk_rate_score` | decimal(19,4) | NOT NULL | risk_rate_score |
| `risk_rating` | varchar(20) | NOT NULL | risk_rating |
| `risk_rate_date` | timestamp(3) | NOT NULL | risk_rate_date |
| `sanction_label` | varchar(128) |  | sanction label |
| `create_time` | timestamp(3) | NOT NULL | create_time |
| `update_time` | timestamp(3) | NOT NULL | update_time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `unique_member_id` 唯一 (member_id)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
