---
id: tbl_installmentcard_t_ic_stl_early_settlement_loan
object_type: Table
name: Per-loan breakdown for early settlement (t_ic_stl_early_settlement_loan)
aliases: [t_ic_stl_early_settlement_loan, installmentcard.t_ic_stl_early_settlement_loan]
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

# Per-loan breakdown for early settlement (t_ic_stl_early_settlement_loan)

## 用途
物理表 `installmentcard.t_ic_stl_early_settlement_loan`,主键 `id`。Per-loan breakdown for early settlement。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `early_settlement_id` | bigint | Ref to t_ic_stl_early_settlement.id |
| `loan_id` | bigint | Ref to t_ic_lm_order.id |
| `principal_amount` | decimal(18, 2) | Remaining principal for this loan |
| `interest_amount` | decimal(18, 2) | Recalculated interest for this loan |
| `original_interest_amount` | decimal(18, 2) | Original loan interest (full tenure) · 可空 |
| `fee_amount` | decimal(18, 2) | Early settlement fee for this loan |
| `fee_vat_amount` | decimal(18, 2) | VAT on fee for this loan |
| `fine_amount` | decimal(18, 2) | Fines attributed to this loan |
| `lpf_amount` | decimal(18, 2) | LPF allocated to this loan from fine_split · 可空 |
| `lpf_vat_amount` | decimal(18, 2) | VAT on LPF for this loan · 可空 |
| `remaining_principal` | decimal(18, 2) | Snapshot of loan remaining_principal at quote time · 可空 |
| `total_amount` | decimal(18, 2) | Total for this loan |
| `created_at` | datetime | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_loan`:loan_id
- `idx_settlement`:early_settlement_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
