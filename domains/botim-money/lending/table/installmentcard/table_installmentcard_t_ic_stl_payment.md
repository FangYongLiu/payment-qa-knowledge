---
id: tbl_installmentcard_t_ic_stl_payment
object_type: Table
name: Master payment records for statement settlement (t_ic_stl_payment)
aliases: [t_ic_stl_payment, installmentcard.t_ic_stl_payment]
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

# Master payment records for statement settlement (t_ic_stl_payment)

## 用途
物理表 `installmentcard.t_ic_stl_payment`,主键 `id`。Master payment records for statement settlement。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `account_id` | bigint | Logical ref to t_ic_am_account.id (no FK) |
| `statement_id` | bigint | Logical ref to t_ic_stm_statement.id (no FK). NULL if unallocated · 可空 |
| `source_credit_id` | bigint | Logical ref to t_ic_stl_overpayment_credit.id (no FK). Used when payment_channel=CREDIT · 可空 |
| `payment_ref` | varchar(150) | Unique gateway/settlement reference for idempotency |
| `payment_channel` | tinyint | Payment channel: 0=WALLET, 1=CARD, 2=BANK_TRANSFER, 3=CASH, 4=OTHER, 5=CREDIT |
| `amount` | decimal(18, 2) | Payment amount |
| `currency` | varchar(3) | Currency (ISO 4217, e.g., AED) |
| `payment_time` | datetime | Time when payment was received/recorded |
| `payment_status` | tinyint | Payment status: 0=SUCCESS, 1=FAILED, 2=REVERSED |
| `raw_payload` | json | Raw gateway payload or settlement metadata (optional) · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_payment_ref`:payment_ref (UNIQUE)
- `idx_account_time`:account_id, payment_time
- `idx_source_credit_id`:source_credit_id
- `idx_statement`:statement_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
