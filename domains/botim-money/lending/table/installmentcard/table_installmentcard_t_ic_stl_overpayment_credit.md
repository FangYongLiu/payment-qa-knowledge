---
id: tbl_installmentcard_t_ic_stl_overpayment_credit
object_type: Table
name: Account credit from overpayment. Applied to future statements automatically (t_ic_stl_overpayment_credit)
aliases: [t_ic_stl_overpayment_credit, installmentcard.t_ic_stl_overpayment_credit]
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

# Account credit from overpayment. Applied to future statements automatically (t_ic_stl_overpayment_credit)

## 用途
物理表 `installmentcard.t_ic_stl_overpayment_credit`,主键 `id`。Account credit from overpayment. Applied to future statements automatically。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `account_id` | bigint | Logical ref to t_ic_am_account.id (no FK) |
| `source_payment_id` | bigint | Payment that created this credit (logical ref to t_ic_stl_payment.id, no FK). NULL for manual adjustments · 可空 |
| `credit_amount` | decimal(18, 2) | Total credited amount from overpayment |
| `remaining_amount` | decimal(18, 2) | Remaining amount available for future statements |
| `currency` | varchar(3) | Currency (ISO 4217, e.g., AED) |
| `credit_status` | tinyint | Credit status: 0=ACTIVE, 1=CONSUMED, 2=REVERSED |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_account_status`:account_id
- `idx_source_payment_id`:source_payment_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
