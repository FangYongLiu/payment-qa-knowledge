---
id: tbl_installmentcard_t_ic_ch_fine_split
object_type: Table
name: Fine allocation splits — tracks how fines are distributed to loans/installments (t_ic_ch_fine_split)
aliases: [t_ic_ch_fine_split, installmentcard.t_ic_ch_fine_split]
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

# Fine allocation splits — tracks how fines are distributed to loans/installments (t_ic_ch_fine_split)

## 用途
物理表 `installmentcard.t_ic_ch_fine_split`,主键 `id`。Fine allocation splits — tracks how fines are distributed to loans/installments。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `account_id` | bigint | FK to account |
| `pending_charge_id` | bigint | FK to t_ic_ch_pending_charge — the source fine |
| `charge_type` | tinyint | Charge type: 0=LATE_FEE, mirrors pending_charge.charge_type |
| `statement_id` | bigint | Statement that triggered the fine |
| `loan_id` | bigint | FK to t_ic_lm_order |
| `installment_id` | bigint | FK to t_ic_lm_installment — NULL when split_level=LOAN · 可空 |
| `split_level` | tinyint | 0=INSTALLMENT, 1=LOAN |
| `split_amount` | decimal(18, 2) | Allocated fine amount (excl. VAT) |
| `vat_amount` | decimal(18, 2) | VAT on this split |
| `billing_status` | tinyint | 0=UNBILLED, 1=BILLED |
| `payment_status` | tinyint | 0=UNPAID, 1=PAID, 2=PARTIALLY_PAID |
| `paid_amount` | decimal(18, 2) | Amount paid so far |
| `created_at` | datetime | 待补 |
| `updated_at` | datetime | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_fine_split_account`:account_id
- `idx_fine_split_installment`:installment_id
- `idx_fine_split_loan`:loan_id
- `idx_fine_split_pending_charge`:pending_charge_id
- `idx_fine_split_statement`:statement_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
