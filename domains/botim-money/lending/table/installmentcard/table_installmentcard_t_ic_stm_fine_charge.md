---
id: tbl_installmentcard_t_ic_stm_fine_charge
object_type: Table
name: Pending charges (LPF, Overlimit) detected between statements (t_ic_stm_fine_charge)
aliases: [t_ic_stm_fine_charge, installmentcard.t_ic_stm_fine_charge]
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

# Pending charges (LPF, Overlimit) detected between statements (t_ic_stm_fine_charge)

## 用途
物理表 `installmentcard.t_ic_stm_fine_charge`,主键 `id`。Pending charges (LPF, Overlimit) detected between statements。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `account_id` | bigint | Account identifier (logical ref to t_ic_am_account.id, no FK) |
| `currency` | varchar(3) | Currency (ISO 4217, e.g., AED) |
| `charge_type` | tinyint | Charge type: 0=LATE_FEE, 1=OVERLIMIT_FEE, 2=OTHER_FEE |
| `basis_type` | tinyint | Basis type: 0=STATEMENT, 1=ACCOUNT (optional) · 可空 |
| `basis_ref_id` | bigint | Reference id for basis (e.g., overdue statement_id for LATE_FEE). No FK · 可空 |
| `product_version_id` | bigint | Product version for fee rules (logical ref to t_ic_pm_product_version.id, no FK) |
| `calculated_amount` | decimal(18, 2) | Base charge amount |
| `vat_amount` | decimal(18, 2) | VAT amount |
| `outstanding_amount` | decimal(18, 2) | Outstanding amount to be billed (charge + VAT) |
| `charge_status` | tinyint | Charge status: 0=PENDING, 1=BILLED, 2=WAIVED |
| `charge_event_time` | datetime | When charge was detected/generated |
| `billed_statement_id` | bigint | Statement where billed (logical ref to t_ic_stm_statement.id, no FK) · 可空 |
| `billed_time` | datetime | When billed into statement · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_charge_idempotency`:account_id, charge_type, basis_type, basis_ref_id (UNIQUE)
- `idx_basis`:basis_type, basis_ref_id
- `idx_billed_statement`:billed_statement_id
- `idx_event_time`:charge_event_time

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
