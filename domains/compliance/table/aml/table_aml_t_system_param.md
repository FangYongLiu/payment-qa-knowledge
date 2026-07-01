---
id: tbl_aml_t_system_param
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
- t_system_param
subdomain: aml
module: null
sensitivity: normal
name: 系统参数表(t_system_param)
aliases:
- t_system_param
related_services:
- svc_aml
related_scenarios: []
---
# 系统参数表(t_system_param)

## 用途
系统参数表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `param_key` | varchar(64) | PK / NOT NULL | 系统业务自定义KEY |
| `param_value` | varchar(512) | PK / NOT NULL | Custom business value |
| `mark` | varchar(256) |  | mark |

## 主键 / 索引
- 主键:(`param_key`, `param_value`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
