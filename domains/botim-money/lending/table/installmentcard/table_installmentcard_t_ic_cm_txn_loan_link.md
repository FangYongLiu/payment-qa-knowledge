---
id: tbl_installmentcard_t_ic_cm_txn_loan_link
object_type: Table
name: Idempotency mapping: guarantees 1 card txn -> 1 loan (t_ic_cm_txn_loan_link)
aliases: [t_ic_cm_txn_loan_link, installmentcard.t_ic_cm_txn_loan_link]
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

# Idempotency mapping: guarantees 1 card txn -> 1 loan (t_ic_cm_txn_loan_link)

## 用途
物理表 `installmentcard.t_ic_cm_txn_loan_link`,主键 `id`。Idempotency mapping: guarantees 1 card txn -> 1 loan。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `txn_id` | bigint | Card transaction id (logical reference to t_ic_cm_card_txn.id; no FK constraint) |
| `loan_id` | bigint | Loan id (NULL until loan created; logical reference to t_ic_lm_loan.id; no FK constraint) · 可空 |
| `link_status` | tinyint | Loan link status: 0=INITIATED (pending loan creation), 1=LINKED (loan created), 2=FAILED (max retries exceeded) |
| `idempotency_key` | varchar(64) | Optional idempotency key used during loan creation (if available) · 可空 |
| `request_id` | varchar(64) | Optional request/trace id for debugging & audit (e.g., X-Request-Id) · 可空 |
| `error_code` | varchar(50) | Error code if loan linking failed (optional) · 可空 |
| `error_message` | varchar(255) | Error message if loan linking failed (optional) · 可空 |
| `retry_count` | tinyint | Number of loan creation retry attempts |
| `next_retry_at` | datetime | Next retry scheduled time (for exponential backoff) · 可空 |
| `last_retry_at` | datetime | Last retry attempt time · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_loan_id`:loan_id (UNIQUE)
- `uk_txn_id`:txn_id (UNIQUE)
- `idx_created_at`:created_at
- `idx_request_id`:request_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
