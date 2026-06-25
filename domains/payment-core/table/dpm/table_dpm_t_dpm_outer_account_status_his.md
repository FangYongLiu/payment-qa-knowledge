---
id: tbl_dpm_t_dpm_outer_account_status_his
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
- t_dpm_outer_account_status_his
subdomain: dpm
module: null
sensitivity: normal
name: 外部账户状态变更记录表(t_dpm_outer_account_status_his)
aliases:
- t_dpm_outer_account_status_his
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 外部账户状态变更记录表(t_dpm_outer_account_status_his)

## 用途
外部账户状态变更记录表。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `HIS_ID` | bigint | PK / NOT NULL | 主键 |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 账户号 |
| `STATUS_MAP` | varchar(6) | NOT NULL | 状态 |
| `PRE_STATUS_MAP` | varchar(6) |  | 变更前状态 |
| `UPDATE_TIME` | timestamp |  | 变更时间 |
| `UPDATE_USER` | varchar(128) |  | 变更人 |
| `MEMO` | varchar(256) |  | 备注 |
| `CLIENT_ID` | varchar(32) |  | 调用方 |

## 主键 / 索引
- 主键:(`HIS_ID`)
- 索引:
  - `idx_account_status_his_account_no` (ACCOUNT_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
