---
id: tbl_aml_t_riskresult_sendconf_items
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
- t_riskresult_sendconf_items
subdomain: aml
module: null
sensitivity: normal
name: 风控事件最终结果通知配置明细表(t_riskresult_sendconf_items)
aliases:
- t_riskresult_sendconf_items
related_services:
- svc_aml
related_scenarios: []
---
# 风控事件最终结果通知配置明细表(t_riskresult_sendconf_items)

## 用途
风控事件最终结果通知配置明细表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL |  |
| `platform_event_type` | varchar(64) | NOT NULL | 事件类型 |
| `values` | varchar(1024) |  | value1,value2,value3,value..n |
| `desc` | varchar(64) |  | value说明 |
| `ops_type` | tinyint | NOT NULL | 类型，1：email，2：手机 |
| `status` | varchar(32) | NOT NULL | valid 有效，invalid 无效 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx1` (platform_event_type)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
