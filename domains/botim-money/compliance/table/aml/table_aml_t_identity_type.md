---
id: tbl_aml_t_identity_type
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
- t_identity_type
subdomain: aml
module: null
sensitivity: normal
name: 核身方式表(t_identity_type)
aliases:
- t_identity_type
related_services:
- svc_aml
related_scenarios: []
---
# 核身方式表(t_identity_type)

## 用途
核身方式表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `identity_type` | varchar(64) | NOT NULL / 默认 '' | 核身方式 |
| `inner_out` | varchar(10) | NOT NULL / 默认 '0' | 所属内外部-INTERNAL:内部;EXTERNAL:外部 |
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
