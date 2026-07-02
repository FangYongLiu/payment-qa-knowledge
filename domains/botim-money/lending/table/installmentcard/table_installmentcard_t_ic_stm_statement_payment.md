---
id: tbl_installmentcard_t_ic_stm_statement_payment
object_type: Table
name: Statement-level payment receipts from gateway/settlement (t_ic_stm_statement_payment)
aliases: [t_ic_stm_statement_payment, installmentcard.t_ic_stm_statement_payment]
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

# Statement-level payment receipts from gateway/settlement (t_ic_stm_statement_payment)

## 用途
物理表 `installmentcard.t_ic_stm_statement_payment`,主键 `id`。Statement-level payment receipts from gateway/settlement。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `statement_id` | bigint | Statement identifier (logical ref to t_ic_stm_statement.id, no FK) |
| `account_id` | bigint | Account identifier (logical ref to t_ic_am_account.id, no FK) |
| `payment_ref` | varchar(100) | Unique external reference from gateway/settlement (idempotency + audit) |
| `amount` | decimal(18, 2) | Payment amount received against the statement |
| `currency` | varchar(3) | Payment currency (ISO 4217, e.g., AED) |
| `payment_time` | datetime | Time when payment was made/received |
| `payment_status` | tinyint | Payment status: 0=SUCCESS, 1=FAILED, 2=REVERSED |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_payment_ref`:payment_ref (UNIQUE)
- `idx_account_id`:account_id
- `idx_payment_time`:payment_time
- `idx_statement_id`:statement_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
