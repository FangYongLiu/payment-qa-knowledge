---
id: tbl_installmentcard_t_ic_stl_early_settlement
object_type: Table
name: Early settlement master record (t_ic_stl_early_settlement)
aliases: [t_ic_stl_early_settlement, installmentcard.t_ic_stl_early_settlement]
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

# Early settlement master record (t_ic_stl_early_settlement)

## 用途
物理表 `installmentcard.t_ic_stl_early_settlement`,主键 `id`。Early settlement master record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `account_id` | bigint | Ref to t_ic_am_account.id |
| `member_id` | varchar(20) | Member ID |
| `settlement_type` | tinyint | 0=ALL_LOANS, 1=SELECTED_LOANS |
| `total_amount` | decimal(18, 2) | Total early settlement amount |
| `total_principal` | decimal(18, 2) | Sum of remaining principal across loans |
| `total_interest` | decimal(18, 2) | Recalculated interest till settlement date |
| `total_fee` | decimal(18, 2) | Early settlement fee |
| `total_fee_vat` | decimal(18, 2) | VAT on early settlement fee |
| `total_fines` | decimal(18, 2) | Pending unbilled fines (LPF + overlimit) |
| `total_billed_unpaid` | decimal(18, 2) | Outstanding on billed/overdue statements |
| `currency` | varchar(3) | Currency (ISO 4217) |
| `settlement_status` | tinyint | 0=QUOTED, 1=PAYMENT_PENDING, 2=SETTLED, 3=FAILED, 4=EXPIRED |
| `payment_id` | bigint | FK to t_ic_pm_payment — set when settlement is executed · 可空 |
| `quote_valid_until` | date | Quote expires end of this day · 可空 |
| `settled_at` | datetime | When settlement was executed · 可空 |
| `created_at` | datetime | 待补 · 可空 |
| `updated_at` | datetime | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_account`:account_id
- `idx_status`:settlement_status

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
