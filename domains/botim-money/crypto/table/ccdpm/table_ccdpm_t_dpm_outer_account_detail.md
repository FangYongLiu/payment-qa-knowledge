---
id: tbl_ccdpm_t_dpm_outer_account_detail
object_type: Table
name: 客户分户账余额明细 (t_dpm_outer_account_detail)
aliases: [t_dpm_outer_account_detail, ccdpm.t_dpm_outer_account_detail]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 客户分户账余额明细 (t_dpm_outer_account_detail)

## 用途
物理表 `ccdpm.t_dpm_outer_account_detail`,主键 `txn_seq_no`。客户分户账余额明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `txn_seq_no` | varchar(32) | 明细流水号 |
| `sys_trace_no` | varchar(32) | 系统跟踪号 · 可空 |
| `accounting_date` | varchar(8) | 会计日 · 可空 |
| `txn_time` | timestamp(3) | 时间 |
| `account_no` | varchar(32) | 账户号 · 可空 |
| `txn_type` | decimal(1) | 事务类型：0:正常,1:红字,2:蓝字,9:抹帐 · 可空 |
| `txn_dscpt` | varchar(256) | 摘要 · 可空 |
| `change_type` | decimal(1) | 变更类型：1: 借贷,2: 冻结解冻 · 可空 |
| `direction` | decimal(1) | 收支方向：1:加(收入) ,2:减(支出) · 可空 |
| `frozen_flag` | varchar(1) | 冻结标志：1:冻结,2:解冻 · 可空 |
| `currency` | varchar(10) | 币种 · 可空 |
| `txn_amt` | decimal(19, 8) | 交易金额 · 可空 |
| `before_amt` | decimal(19, 8) | 交易前余额 · 可空 |
| `after_amt` | decimal(19, 8) | 交易后余额 · 可空 |
| `accounting_version` | bigint | 记账版本 |
| `entry_seq_no` | varchar(32) | 分录号 · 可空 |
| `other_account_no` | varchar(32) | 对方账号 · 可空 |
| `old_txn_seq_no` | varchar(32) | 原事务号 · 可空 |
| `remark` | varchar(256) | 备注 · 可空 |
| `crdr` | decimal(1) | 借贷标志：1:借,2:贷 · 可空 |
| `product_code` | varchar(12) | 支付产品编码 · 可空 |
| `pay_code` | varchar(12) | 支付编码 · 可空 |
| `operation_type` | decimal(1) | 操作类型 · 可空 |
| `delete_sign` | decimal(1) | 删除标记(冲正用) · 可空 |
| `suite_no` | varchar(32) | 套号：19位transactionNo+2位套号顺序(01开始) · 可空 |
| `context_voucher_no` | varchar(32) | 关联结算流水号 · 可空 |
| `accounting_rule` | decimal(1) | 记账规则：DEFAULT(0, "减钱(付款方):先贷记账户后借记账户,加钱(收款方):借记账户"),                DR(1, "只借记子账户"),                CR(2, "只贷记子账户"),                CRDR(3, "减钱(付款方):先贷记账户后借记账户,加钱(收款方):出款方借记到收款方借记,出款方贷记到收款方贷记") · 可空 |
| `transaction_no` | varchar(32) | 事务号 · 可空 |
| `voucher_no` | varchar(50) | 凭证号：21位记账套号+2位借贷顺序(01开始) · 可空 |
| `payment_voucher_no` | varchar(64) | 支付凭证号 · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |

## 主键 / 索引
- 主键:`txn_seq_no`
- `uk_voucher_no`:voucher_no (UNIQUE)
- `idx_account_no`:account_no
- `idx_account_no_txn_time`:account_no, txn_time
- `idx_sys_trace_no`:sys_trace_no
- `idx_txn_time`:txn_time

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
