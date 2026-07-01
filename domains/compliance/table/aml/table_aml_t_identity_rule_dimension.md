---
id: tbl_aml_t_identity_rule_dimension
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
- t_identity_rule_dimension
subdomain: aml
module: null
sensitivity: normal
name: 核身规则维度表(t_identity_rule_dimension)
aliases:
- t_identity_rule_dimension
related_services:
- svc_aml
related_scenarios: []
---
# 核身规则维度表(t_identity_rule_dimension)

## 用途
核身规则维度表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `event_type` | varchar(50) | NOT NULL | 事件类型 |
| `dimension` | varchar(32) | NOT NULL | 维度 |
| `remarks` | varchar(64) |  | 描述 |
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
