---
id: tbl_installmentcard_t_ic_cm_card_txn
object_type: Table
name: t_ic_cm_card_txn (t_ic_cm_card_txn)
aliases: [t_ic_cm_card_txn, installmentcard.t_ic_cm_card_txn]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# t_ic_cm_card_txn (t_ic_cm_card_txn)

## 用途
物理表 `installmentcard.t_ic_cm_card_txn`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key (internal transaction identifier) · 可空 |
| `card_id` | bigint | Logical reference to t_ic_cm_card.id. No FK constraint |
| `account_id` | bigint | Logical reference to t_ic_am_account.id. No FK constraint |
| `trx_voucher_no` | varchar(64) | PPC transaction voucher number - primary reference for PPC reconciliation · 可空 |
| `transaction_ref` | varchar(100) | Transaction reference from PPC · 可空 |
| `ppc_txn_type` | varchar(10) | PPC transaction type: T, TC, S, FS, R, RL, CB, BR, F, RF · 可空 |
| `dr_cr` | varchar(1) | Debit/Credit indicator from PPC: D=Debit, C=Credit · 可空 |
| `orig_trx_voucher_no` | varchar(64) | Original transaction voucher number (for reversals/adjustments) · 可空 |
| `reversal_trx_voucher_no` | varchar(64) | Reversal transaction voucher number (for reversals/adjustments) · 可空 |
| `merchant_id` | varchar(64) | Merchant identifier from gateway/acquirer (nullable if not provided) · 可空 |
| `merchant_name` | varchar(128) | Merchant name from gateway/acquirer (nullable if not provided) · 可空 |
| `mcc` | varchar(4) | Merchant Category Code (MCC), typically 4 digits · 可空 |
| `requested_amount` | decimal(18, 2) | Amount requested by merchant at auth time (e.g., 300.00) |
| `authorized_amount` | decimal(18, 2) | Total authorized/held amount after approvals/adjustments (e.g., 500.00) · 可空 |
| `captured_amount` | decimal(18, 2) | Total captured amount after clearing/capture (e.g., 450.00) · 可空 |
| `currency` | varchar(3) | Currency code (ISO 4217), e.g., AED |
| `txn_status` | tinyint | Transaction status: 0=RECEIVED, 1=PENDING, 2=AUTHORIZED, 3=DECLINED, 4=CAPTURED, 5=REVERSED, 6=REFUNDED, 7=CANCELLED, 8=FAILED, 9=SETTLED. Note: CAPTURED(4) is the actual capture transaction. SETTLED(9) marks original AUTH consumed by settlement - use CAPTURED to query real captures. |
| `txn_time` | datetime | Transaction time from gateway/PPC (event occurrence time) |
| `received_at` | datetime | System time when this record/event was received. Also serves as posting datestamp |
| `loan_blocked` | tinyint | Loan creation blocked: 0=No, 1=Yes (blocked due to refund arriving before loan creation) |
| `loan_blocked_by_txn_id` | bigint | Refund transaction that blocked loan creation (ref to t_ic_cm_card_txn.id) · 可空 |
| `loan_blocked_at` | datetime | When loan creation was blocked · 可空 |
| `created_at` | datetime | Record creation time |
| `updated_at` | datetime | Record last update time |
| `created_by` | varchar(50) | Service/user that created this record |
| `updated_by` | varchar(50) | Service/user that last updated this record |
| `is_deleted` | tinyint | Soft delete flag: 0=false, 1=true |

## 主键 / 索引
- 主键:`id`
- `uk_trx_voucher_no`:trx_voucher_no (UNIQUE)
- `idx_account_time`:account_id, txn_time
- `idx_card_time`:card_id, txn_time
- `idx_created_at`:created_at
- `idx_orig_trx_voucher`:orig_trx_voucher_no

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
