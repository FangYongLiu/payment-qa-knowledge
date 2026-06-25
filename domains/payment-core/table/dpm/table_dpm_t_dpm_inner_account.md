---
id: tbl_dpm_t_dpm_inner_account
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
- t_dpm_inner_account
subdomain: dpm
module: null
sensitivity: normal
name: 内部账户(t_dpm_inner_account)
aliases:
- t_dpm_inner_account
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 内部账户(t_dpm_inner_account)

## 用途
内部账户。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ACCOUNT_NO` | varchar(32) | PK / NOT NULL | 帐号号 |
| `ACCOUNT_TITLE_NO` | varchar(32) |  | 科目号 |
| `ACCOUNT_NAME` | varchar(100) |  | 账户名称 |
| `OPEN_DATE` | timestamp |  | 开户日期(创建时间) |
| `BAL_DIRECTION` | decimal(1) |  | 1:借 2:贷 0:双向 |
| `CURR_BAL_DIRECTION` | decimal(1) |  | 1:借 2:贷 |
| `CURRENCY_CODE` | varchar(3) |  | 货币类型 |
| `BALANCE` | decimal(19,4) | 默认 0 | 余额 |
| `accounting_version` | bigint | NOT NULL / 默认 0 | 记账版本 |
| `LAST_UPDATE_TIME` | timestamp |  | 最后更新时间 |

## 主键 / 索引
- 主键:(`ACCOUNT_NO`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
