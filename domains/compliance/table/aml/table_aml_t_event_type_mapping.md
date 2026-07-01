---
id: tbl_aml_t_event_type_mapping
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
- t_event_type_mapping
subdomain: aml
module: null
sensitivity: normal
name: 事件类型映射(t_event_type_mapping)
aliases:
- t_event_type_mapping
related_services:
- svc_aml
related_scenarios: []
---
# 事件类型映射(t_event_type_mapping)

## 用途
事件类型映射。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `event_type` | varchar(32) |  | 事件类型 |
| `customer_event_type` | varchar(32) |  | 客户事件类型 |
| `policy` | varchar(32) |  | 策略 |
| `create_time` | timestamp |  | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
