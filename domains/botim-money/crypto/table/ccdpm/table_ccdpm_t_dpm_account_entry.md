---
id: tbl_ccdpm_t_dpm_account_entry
object_type: Table
name: 记账分录 (t_dpm_account_entry)
aliases: [t_dpm_account_entry, ccdpm.t_dpm_account_entry]
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

# 记账分录 (t_dpm_account_entry)

## 用途
物理表 `ccdpm.t_dpm_account_entry`,主键 `entry_seq_no`。记账分录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `entry_seq_no` | varchar(32) | 分录号 |
| `transaction_no` | varchar(32) | 事务号 |
| `suite_no` | varchar(32) | 套号 |
| `voucher_no` | varchar(50) | 凭证号 · 可空 |
| `sys_trace_no` | varchar(32) | 系统跟踪编号 · 可空 |
| `account_no` | varchar(32) | 账号 |
| `title_no` | varchar(32) | 科目号 · 可空 |
| `entry_type` | decimal(1) | 分录类型：0:表内分录,1:表外分录 · 可空 |
| `is_manual` | decimal(1) | 自动手工标志：0:自动,1:手工 · 可空 |
| `txn_currency` | varchar(10) | 币种 · 可空 |
| `amount` | decimal(19, 8) | 金额 |
| `txn_type` | decimal(1) | 事务类型：0-正常,1-红字,2-蓝字,9-抹帐 |
| `direction` | decimal(1) | 借贷标志：1:借,2:贷 |
| `audit_status` | decimal(1) | 审核状态：0-未复核,1-已复核,2-不需事中复核 |
| `status` | decimal(1) | 记账状态：0-未入账,2-已入账,3-已抹帐,9-无效 · 可空 |
| `accounting_date` | varchar(8) | 记账日 |
| `create_time` | timestamp | 创建时间 |
| `last_update_time` | timestamp | 最后更新时间 · 可空 |
| `bal_update_time` | timestamp | 余额更新时间 · 可空 |
| `remark` | varchar(256) | 备注 · 可空 |
| `is_buffer` | decimal(1) | 是否缓冲：0:未缓冲,1:缓冲 · 可空 |
| `old_entry_seq_no` | varchar(32) | 原分录号 · 可空 |
| `summary` | varchar(256) | 摘要 · 可空 |
| `input_uid` | varchar(32) | 录入人 · 可空 |
| `input_time` | timestamp | 录入时间 · 可空 |
| `check_uid` | varchar(32) | 检查人 · 可空 |
| `check_time` | timestamp | 检查时间 · 可空 |
| `rsvd_amt1` | decimal(19, 8) | 保留金额1 · 可空 |
| `rsvd_amt2` | decimal(19, 8) | 保留金额2 · 可空 |
| `rsvd_text1` | varchar(50) | 保留字段1 · 可空 |
| `rsvd_text2` | varchar(50) | 保留字段2 · 可空 |
| `context_voucher_no` | varchar(50) | 关联结算流水号 · 可空 |
| `operater` | decimal(1) | 操作员 · 可空 |
| `clearing_code` | varchar(32) | 清算编码 · 可空 |

## 主键 / 索引
- 主键:`entry_seq_no`
- `idx_create_time`:create_time
- `idx_voucher_no`:voucher_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
