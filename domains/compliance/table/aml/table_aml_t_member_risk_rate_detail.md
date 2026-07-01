---
id: tbl_aml_t_member_risk_rate_detail
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
- t_member_risk_rate_detail
subdomain: aml
module: null
sensitivity: normal
name: 会员风险评级明细(t_member_risk_rate_detail)
aliases:
- t_member_risk_rate_detail
related_services:
- svc_aml
related_scenarios: []
---
# 会员风险评级明细(t_member_risk_rate_detail)

## 用途
会员风险评级明细。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `rate_id` | bigint | NOT NULL | 评级id |
| `rule_id` | bigint | NOT NULL | 规则id |
| `rule_item_id` | bigint | NOT NULL | 命中的规则明细id |
| `risk_point` | int | NOT NULL | 风险点 |
| `risk_score` | decimal(19,4) | NOT NULL | 风险评级分数 |
| `create_time` | timestamp(3) | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_rate_id` (rate_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
