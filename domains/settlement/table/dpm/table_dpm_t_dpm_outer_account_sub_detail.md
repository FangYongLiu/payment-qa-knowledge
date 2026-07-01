---
id: tbl_dpm_t_dpm_outer_account_sub_detail
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
- t_dpm_outer_account_sub_detail
subdomain: dpm
module: null
sensitivity: normal
name: 外部账户分户账户明细(t_dpm_outer_account_sub_detail)
aliases:
- t_dpm_outer_account_sub_detail
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 外部账户分户账户明细(t_dpm_outer_account_sub_detail)

## 用途
外部账户分户账户明细。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ACCOUNT_SUBSET_LOG_ID` | decimal(32) | PK / NOT NULL | 分户账户余额明细 |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 账户号 |
| `FUND_TYPE` | decimal(1) | NOT NULL | 资金类型 1,借记 2.贷记 |
| `BALANCE_TYPE` | decimal(1) | NOT NULL | 余额类型 1.普通 2.冻结 |
| `SYS_TRACE_NO` | varchar(32) |  | 系统跟踪号 |
| `VOUCHER_NO` | varchar(50) | NOT NULL | 凭证号 |
| `CURRENCY` | char(3) |  | 币种 |
| `TXN_AMT` | decimal(19,4) |  | 交易金额 |
| `AFTER_AMT` | decimal(19,4) |  | 交易后余额 |
| `ACCOUNTING_RULE` | decimal(1) | NOT NULL | 入账规则 |
| `REMARK` | varchar(256) |  | 备注 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp | NOT NULL | 更新时间 |
| `DIRECTION` | decimal(1) | NOT NULL | 1:加(收入) 2:减(支出) |

## 主键 / 索引
- 主键:(`ACCOUNT_SUBSET_LOG_ID`)
- 索引:
  - `IDX_ACCOUNT_SUB_DTL_VOUCH` (VOUCHER_NO)
  - `IDX_ACCT_SUB_DTL_SYS_TRACE_NO` (SYS_TRACE_NO)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
