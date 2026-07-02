---
id: tbl_installmentcard_t_ic_cm_txn_refund_link
object_type: Table
name: Refund settlement tracking: guarantees async processing with retry (t_ic_cm_txn_refund_link)
aliases: [t_ic_cm_txn_refund_link, installmentcard.t_ic_cm_txn_refund_link]
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

# Refund settlement tracking: guarantees async processing with retry (t_ic_cm_txn_refund_link)

## 用途
物理表 `installmentcard.t_ic_cm_txn_refund_link`,主键 `id`。Refund settlement tracking: guarantees async processing with retry。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `refund_txn_id` | bigint | Refund transaction id (logical reference to t_ic_cm_card_txn.id; no FK constraint) |
| `original_txn_id` | bigint | Original settlement transaction id (may be NULL if not found) · 可空 |
| `account_id` | bigint | Account ID (logical reference to t_ic_am_account.id; no FK constraint) |
| `loan_id` | bigint | Loan id settled against (NULL until settled; logical reference to t_ic_lm_order.id; no FK constraint) · 可空 |
| `refund_amount` | decimal(18, 2) | Total refund amount |
| `settled_amount` | decimal(18, 2) | Amount settled against installments · 可空 |
| `excess_amount` | decimal(18, 2) | Excess amount credited to wallet · 可空 |
| `currency` | varchar(3) | Currency code (ISO 4217) |
| `link_status` | tinyint | Status: 0=INITIATED, 1=SETTLED, 2=FAILED, 3=LOAN_BLOCKED, 4=WALLET_CREDITED |
| `idempotency_key` | varchar(64) | Idempotency key (request_id) · 可空 |
| `request_id` | varchar(64) | Request/trace id for debugging & audit · 可空 |
| `error_code` | varchar(50) | Error code if settlement failed · 可空 |
| `error_message` | varchar(255) | Error message if settlement failed · 可空 |
| `retry_count` | tinyint | Number of settlement retry attempts |
| `next_retry_at` | datetime | Next retry scheduled time (for exponential backoff) · 可空 |
| `last_retry_at` | datetime | Last retry attempt time · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_refund_txn_id`:refund_txn_id (UNIQUE)
- `idx_account_id`:account_id
- `idx_loan_id`:loan_id
- `idx_original_txn_id`:original_txn_id
- `idx_request_id`:request_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
