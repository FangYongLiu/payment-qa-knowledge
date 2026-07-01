---
id: tbl_aml_t_risk_status_score
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
- t_risk_status_score
subdomain: aml
module: null
sensitivity: normal
name: 风险状态分数表(t_risk_status_score)
aliases:
- t_risk_status_score
related_services:
- svc_aml
related_scenarios: []
---
# 风险状态分数表(t_risk_status_score)

## 用途
风险状态分数表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL |  |
| `final_result` | varchar(10) | NOT NULL | 最终结果：PASS/CHALLENGE/REJECT |
| `min_score` | int | NOT NULL | 最小分数 |
| `max_score` | int | NOT NULL | 最大分数 |
| `to_risk_identity` | tinyint(1) | 默认 0 | 是否走核身：0.不走；1.走 |
| `status` | int | 默认 1 | 状态：0.停用;1.生效;2.草稿;3.试运行; |
| `event_type` | varchar(100) |  | 事件类型 |
| `related_id` | bigint |  | 关联ID |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |
| `create_by` | varchar(32) |  | 创建者 |
| `update_by` | varchar(32) |  | 更新者 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
