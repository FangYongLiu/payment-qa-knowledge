---
id: tbl_ppcenter_t_data_apply
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_data_apply
subdomain: pricing
module: null
sensitivity: normal
name: 数据申请(t_data_apply)
aliases:
- t_data_apply
related_services:
- svc_ppcenter
related_scenarios: []
---
# 数据申请(t_data_apply)

## 用途
数据申请。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | primary key |
| `step` | varchar(12) |  | step（gateway, calculation, clearing, pay_auth,success) |
| `status` | varchar(1) | NOT NULL | I:Submission successful; P:Processing; E:EXCEPTION; F:FAIL；S:SUCCESS |
| `gmt_effective` | timestamp |  | effectiv time |
| `gmt_invalid` | timestamp |  | invalid time |
| `gmt_create` | timestamp | NOT NULL | create time |
| `gmt_modify` | timestamp | NOT NULL | update time |
| `apply_id` | int(12) |  | 申请id |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
