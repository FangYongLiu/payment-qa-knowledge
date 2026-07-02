---
id: tbl_installmentcard_t_ic_am_limit_ledger
object_type: Table
name: Ledger tracking all limit changes with before/after state (t_ic_am_limit_ledger)
aliases: [t_ic_am_limit_ledger, installmentcard.t_ic_am_limit_ledger]
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

# Ledger tracking all limit changes with before/after state (t_ic_am_limit_ledger)

## 用途
物理表 `installmentcard.t_ic_am_limit_ledger`,主键 `id`。Ledger tracking all limit changes with before/after state。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(32) | Card holder member id |
| `account_id` | bigint | Account ID |
| `ref_type` | varchar(20) | Source type: TXN, PAYMENT, ADJUSTMENT, ADMIN |
| `ref_id` | bigint | Source ID (txn_id, payment_id, etc.) · 可空 |
| `trx_voucher_no` | varchar(64) | Transaction voucher for quick lookup · 可空 |
| `event_type` | varchar(30) | Event that caused change |
| `wallet_command` | varchar(2) | PPC wallet command: F, U, UD, D, C · 可空 |
| `amount` | decimal(18, 2) | Change amount (always positive) |
| `currency` | varchar(3) | 待补 |
| `pending_change` | decimal(18, 2) | Change to limit_pending (+/-) |
| `used_change` | decimal(18, 2) | Change to limit_used (+/-) |
| `available_change` | decimal(18, 2) | Change to limit_available (+/-) |
| `pending_after` | decimal(18, 2) | limit_pending after this event |
| `used_after` | decimal(18, 2) | limit_used after this event |
| `available_after` | decimal(18, 2) | limit_available after this event |
| `idempotency_key` | varchar(64) | Unique key to prevent duplicates |
| `occurred_at` | datetime(3) | When event occurred |
| `created_at` | datetime(3) | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_idempotency_key`:idempotency_key (UNIQUE)
- `idx_account_id`:account_id
- `idx_occurred_at`:occurred_at
- `idx_ref_type_ref_id`:ref_id, ref_type
- `idx_trx_voucher_no`:trx_voucher_no

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
