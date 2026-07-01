---
id: tbl_dpm_dbajobconf
object_type: Table
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (dpm schema) 2026-06-25
tags:
- dpm
- dpm
- dbajobconf
subdomain: dpm
module: null
sensitivity: normal
name: dbajobconf
aliases:
- dbajobconf
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# dbajobconf

## 用途
待补。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `JOBNAME` | varchar(50) | PK / NOT NULL | 作业名字 |
| `JOBSTATUS` | varchar(20) |  | 作业进度 |
| `COMMENTS` | varchar(50) |  | 注释 |

## 主键 / 索引
- 主键:(`JOBNAME`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
