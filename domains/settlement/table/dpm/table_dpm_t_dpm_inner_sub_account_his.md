---
id: tbl_dpm_t_dpm_inner_sub_account_his
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
- t_dpm_inner_sub_account_his
subdomain: dpm
module: null
sensitivity: normal
name: 内部账户分户表 历史表(t_dpm_inner_sub_account_his)
aliases:
- t_dpm_inner_sub_account_his
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 内部账户分户表 历史表(t_dpm_inner_sub_account_his)

## 用途
内部账户分户表 历史表。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `HIS_ID` | decimal(17) | PK / NOT NULL |  |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 账号 |
| `BALANCE` | decimal(19,4) | NOT NULL | 余额 |
| `BIZ_NO` | varchar(32) | NOT NULL | 业务号 |
| `PID` | varchar(10) | NOT NULL | 平台ID |
| `REMARK` | varchar(256) |  | 备注 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`HIS_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
