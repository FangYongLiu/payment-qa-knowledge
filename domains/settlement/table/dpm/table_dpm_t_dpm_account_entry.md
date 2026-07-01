---
id: tbl_dpm_t_dpm_account_entry
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
- t_dpm_account_entry
subdomain: dpm
module: null
sensitivity: normal
name: 会计分录(表内/表外)(t_dpm_account_entry)
aliases:
- t_dpm_account_entry
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 会计分录(表内/表外)(t_dpm_account_entry)

## 用途
会计分录(表内/表外)。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ENTRY_SEQ_NO` | varchar(32) | PK / NOT NULL | 分录号 |
| `TRANSACTION_NO` | varchar(32) | NOT NULL | 事务号 |
| `SUITE_NO` | varchar(32) | NOT NULL | 套号 |
| `VOUCHER_NO` | varchar(50) |  | 凭证号 |
| `SYS_TRACE_NO` | varchar(32) |  | 系统跟踪编号 |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 账号 |
| `TITLE_NO` | varchar(32) |  | 科目号 |
| `ENTRY_TYPE` | decimal(1) |  | 0:表内分录 1:表外分录 |
| `IS_MANUAL` | decimal(1) |  | 自动手工标志 0:自动 1:手工 |
| `TXN_CURRENCY` | varchar(3) |  | 币种 |
| `AMOUNT` | decimal(19,4) | NOT NULL | 金额 |
| `TXN_TYPE` | decimal(1) | NOT NULL | 0-正常 1-红字 2-蓝字 9-抹帐 |
| `DIRECTION` | decimal(1) | NOT NULL | 1:借 2:贷 |
| `AUDIT_STATUS` | decimal(1) | NOT NULL | 0-未复核 1-已复核 2-不需事中复核 |
| `STATUS` | decimal(1) |  | 0-未入账 2-已入账 3-已抹帐 9-无效 |
| `ACCOUNTING_DATE` | varchar(8) | NOT NULL | 记账日 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `LAST_UPDATE_TIME` | timestamp |  | 最后更新时间 |
| `BAL_UPDATE_TIME` | timestamp |  | 余额更新时间 |
| `REMARK` | varchar(256) |  | 备注 |
| `IS_BUFFER` | decimal(1) |  | 0:未缓冲 1:缓冲 |
| `OLD_ENTRY_SEQ_NO` | varchar(32) |  | 原分录号 |
| `SUMMARY` | varchar(256) |  | 摘要 |
| `INPUT_UID` | varchar(32) |  | 录入人 |
| `INPUT_TIME` | timestamp |  | 录入时间 |
| `CHECK_UID` | varchar(32) |  | 检查人 |
| `CHECK_TIME` | timestamp |  | 检查时间 |
| `RSVD_AMT1` | decimal(19,4) | 默认 0 | 保留金额1 |
| `RSVD_AMT2` | decimal(19,4) | 默认 0 | 保留金额2 |
| `RSVD_TEXT1` | varchar(50) |  | 保留字段1 |
| `RSVD_TEXT2` | varchar(50) |  | 保留字段2 |
| `CONTEXT_VOUCHER_NO` | varchar(50) |  | 关联结算流水号 |
| `OPERATER` | decimal(1) |  | 操作员 |
| `CLEARING_CODE` | varchar(32) |  | 清算编码 |

## 主键 / 索引
- 主键:(`ENTRY_SEQ_NO`)
- 索引:
  - `UK_ENTRY_VOUCHER_NO` (VOUCHER_NO)
  - `inx_entry_ct` (CREATE_TIME)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
