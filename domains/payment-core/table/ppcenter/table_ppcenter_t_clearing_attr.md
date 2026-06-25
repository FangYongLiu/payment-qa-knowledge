---
id: tbl_ppcenter_t_clearing_attr
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_clearing_attr
subdomain: pricing
module: null
sensitivity: normal
name: 清结算周期属性(t_clearing_attr)
aliases:
- t_clearing_attr
related_services:
- svc_ppcenter
related_scenarios: []
---
# 清结算周期属性(t_clearing_attr)

## 用途
清结算周期属性。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `clearing_id` | int | NOT NULL | 结算模板id |
| `key` | varchar(64) | NOT NULL | 扩展字段key |
| `value` | varchar(128) | NOT NULL | 扩展字段value |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
