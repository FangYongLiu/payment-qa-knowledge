---
id: tbl_dpm_t_dpm_management_log
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
- t_dpm_management_log
subdomain: dpm
module: null
sensitivity: normal
name: 账户管理日志(t_dpm_management_log)
aliases:
- t_dpm_management_log
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 账户管理日志(t_dpm_management_log)

## 用途
账户管理日志。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TXN_SEQ_NO` | varchar(32) | PK / NOT NULL | 事务号 |
| `SYS_TRACE_NO` | varchar(32) |  | 系统跟踪编号 |
| `ACCOUNT_ID` | varchar(32) |  | 账号 |
| `TXN_TYPE` | varchar(6) |  | 类型 |
| `TXN_DSCPT` | varchar(256) |  | 事务描述 |
| `BEFORE_STATUS` | varchar(6) |  | 前状态 |
| `AFTER_STATUS` | varchar(6) |  | 后状态 |
| `REMARK` | varchar(256) |  | 备注 |
| `INPUT_UID` | varchar(32) |  | 录入人 |
| `INPUT_TIME` | timestamp |  | 录入时间 |
| `CHECK_UID` | varchar(32) |  | 检查人 |
| `CHECK_TIME` | timestamp |  | 检查时间 |
| `RESV_FLD1` | varchar(50) |  | 保留1 |
| `RESV_FLD2` | varchar(50) |  | 保留2 |
| `RESV_FLD3` | varchar(50) |  | 保留3 |

## 主键 / 索引
- 主键:(`TXN_SEQ_NO`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
