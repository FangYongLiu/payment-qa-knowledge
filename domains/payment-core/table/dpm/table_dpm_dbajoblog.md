---
id: tbl_dpm_dbajoblog
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (dpm schema) 2026-06-25
tags:
- dpm
- dpm
- dbajoblog
subdomain: dpm
module: null
sensitivity: normal
name: dbajoblog
aliases:
- dbajoblog
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# dbajoblog

## 用途
待补。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `JOBID` | decimal(8) | PK / NOT NULL | 任务ID |
| `JOBNAME` | varchar(50) |  | 任务名 |
| `STARTDATE` | timestamp |  | 开始时间 |
| `ENDDATE` | timestamp |  | 结束时间 |
| `JOBSTATUS` | varchar(20) |  | 任务状态 |
| `COMMENTS` | varchar(100) |  | 注释 |
| `PARAMETER` | varchar(100) |  | 参数 |

## 主键 / 索引
- 主键:(`JOBID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
