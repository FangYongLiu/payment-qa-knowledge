---
id: tbl_dpm_t_job_progress
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
- t_job_progress
subdomain: dpm
module: null
sensitivity: normal
name: 任务进度(t_job_progress)
aliases:
- t_job_progress
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 任务进度(t_job_progress)

## 用途
任务进度。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `job_code` | varchar(128) | PK / NOT NULL | 任务代码 |
| `job_desc` | varchar(1024) | NOT NULL | 任务描述 |
| `job_progress` | varchar(128) | NOT NULL | 任务进度 |
| `extension` | varchar(1024) |  | 扩展参数 |
| `memo` | varchar(1024) |  | 备注 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`job_code`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
