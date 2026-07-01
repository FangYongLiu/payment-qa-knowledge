---
id: tbl_aml_t_risk_rate_point_config
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
- t_risk_rate_point_config
subdomain: aml
module: null
sensitivity: normal
name: 风险评级配置表(t_risk_rate_point_config)
aliases:
- t_risk_rate_point_config
related_services:
- svc_aml
related_scenarios: []
---
# 风险评级配置表(t_risk_rate_point_config)

## 用途
风险评级配置表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `min_score` | decimal(19,4) | NOT NULL | 最小分数 |
| `max_score` | decimal(19,4) | NOT NULL | 最大分数 |
| `risk_rating` | varchar(10) | NOT NULL | 风险等级 |
| `due_diligence_level` | varchar(20) | NOT NULL | 尽职调查级别 |
| `need_check` | char | NOT NULL | 是否需要审核 |
| `due_diligence_cycle` | decimal(19,4) | NOT NULL | 尽职调查周期（单位：年） |
| `create_time` | timestamp(3) | NOT NULL | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
