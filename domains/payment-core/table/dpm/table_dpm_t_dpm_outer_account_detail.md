---
id: tbl_dpm_t_dpm_outer_account_detail
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
- t_dpm_outer_account_detail
subdomain: dpm
module: null
sensitivity: normal
name: 客户分户账余额明细(t_dpm_outer_account_detail)
aliases:
- t_dpm_outer_account_detail
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 客户分户账余额明细(t_dpm_outer_account_detail)

## 用途
客户分户账余额明细。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TXN_SEQ_NO` | varchar(32) | PK / NOT NULL | 明细流水号 |
| `SYS_TRACE_NO` | varchar(32) |  | 系统跟踪号 |
| `ACCOUNTING_DATE` | varchar(8) |  | 会计日 |
| `txn_time` | timestamp(3) | NOT NULL / 默认 CURRENT_TIMESTAMP(3) | 时间 |
| `ACCOUNT_NO` | varchar(32) |  | 账户号 |
| `TXN_TYPE` | decimal(1) |  | 0:正常 1:红字 2:蓝字 9:抹帐 |
| `TXN_DSCPT` | varchar(256) |  | 摘要 |
| `CHANGE_TYPE` | decimal(1) |  | 1: 借贷 2: 冻结解冻 |
| `DIRECTION` | decimal(1) |  | 1:加(收入) 2:减(支出) |
| `FROZEN_FLAG` | varchar(1) |  | 1:冻结 2:解冻 |
| `CURRENCY` | char(3) |  | 币种 |
| `TXN_AMT` | decimal(19,4) |  | 交易金额 |
| `BEFORE_AMT` | decimal(19,4) |  | 交易前余额 |
| `AFTER_AMT` | decimal(19,4) |  | 交易后余额 |
| `accounting_version` | bigint | NOT NULL / 默认 0 | 记账版本 |
| `ENTRY_SEQ_NO` | varchar(32) |  | 分录号 |
| `OTHER_ACCOUNT_NO` | varchar(32) |  | 对方账号 |
| `OLD_TXN_SEQ_NO` | varchar(32) |  | 原事务号 |
| `REMARK` | varchar(256) |  | 备注 |
| `CRDR` | decimal(1) |  | 借贷标志 1借2贷 |
| `PRODUCT_CODE` | varchar(12) |  | PE产品编码 |
| `PAY_CODE` | varchar(12) |  | PE支付编码 |
| `OPERATION_TYPE` | decimal(1) |  | 操作类型 |
| `DELETE_SIGN` | decimal(1) |  | 删除标记(冲正用) |
| `SUITE_NO` | varchar(32) |  | 套号 |
| `CONTEXT_VOUCHER_NO` | varchar(32) |  | 关联结算流水号 |
| `ACCOUNTING_RULE` | decimal(1) |  | 入账规则 0:默认 1:只借记 2:只贷记 3:混合 |
| `TRANSACTION_NO` | varchar(32) |  | 事务号 |
| `VOUCHER_NO` | varchar(50) |  | 凭证号 |
| `PAYMENT_VOUCHER_NO` | varchar(64) |  | 对应统一凭证里的支付凭证号 |
| `extension` | varchar(255) |  | 扩展信息 |

## 主键 / 索引
- 主键:(`TXN_SEQ_NO`)
- 唯一约束:
  - `UIDX_OAD_VO` 唯一 (VOUCHER_NO)
- 索引:
  - `IDX_ACCOUNTNO_VERSION` (ACCOUNT_NO, accounting_version)
  - `IDX_DOAD_STN` (SYS_TRACE_NO)
  - `IDX_DOAD_TXN_TIME` (txn_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
