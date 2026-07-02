---
id: tbl_installmentcard_t_ic_pm_product_version
object_type: Table
name: Effective-dated product rules (t_ic_pm_product_version)
aliases: [t_ic_pm_product_version, installmentcard.t_ic_pm_product_version]
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

# Effective-dated product rules (t_ic_pm_product_version)

## 用途
物理表 `installmentcard.t_ic_pm_product_version`,主键 `id`。Effective-dated product rules。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key of product version · 可空 |
| `product_id` | bigint | Product identifier (logical ref to t_ic_pm_product.id, no FK) |
| `version_no` | int | Monotonic version number (optional alternative to version_code) · 可空 |
| `version_code` | varchar(50) | Version code (optional alternative to version_no) · 可空 |
| `effective_from` | datetime | Rule effective start datetime |
| `effective_to` | datetime | Rule effective end datetime (NULL = open-ended) · 可空 |
| `interest_type` | tinyint | Interest type: 0=FLAT, 1=REDUCING (NULL for Model A) · 可空 |
| `interest_rate` | decimal(10, 6) | Interest rate for the tenure (e.g., 0.2533 for 25.33%) · 可空 |
| `tenure_min_months` | int | Minimum tenure / number of installments |
| `tenure_max_months` | int | Maximum tenure / number of installments |
| `allowed_tenures_json` | varchar(500) | JSON list of allowed tenures with rates · 可空 |
| `processing_fee_type` | tinyint | Fee type: 0=FIXED, 1=PERCENTAGE, 2=PERCENTAGE_WITH_CAP |
| `processing_fee_value` | decimal(10, 4) | Fee amount (FIXED) or rate (PERCENTAGE) |
| `processing_fee_min` | decimal(18, 2) | Minimum fee (nullable) · 可空 |
| `processing_fee_max` | decimal(18, 2) | Maximum fee (nullable) · 可空 |
| `late_fee_basis` | tinyint | Late fee basis: 0=STATEMENT, 1=INSTALLMENT |
| `late_fee_frequency` | tinyint | Frequency: 0=ONCE_PER_STATEMENT, 1=PER_CYCLE, 2=DAILY |
| `late_fee_apply_after_days` | int | Apply after N days past due (PRD: 1) |
| `late_fee_type` | tinyint | Fee type: 0=FIXED, 1=PERCENTAGE, 2=PERCENTAGE_WITH_CAP |
| `late_fee_value` | decimal(10, 4) | Fee amount (PRD: 230.00 AED) |
| `late_fee_min` | decimal(18, 2) | Minimum fee (nullable) · 可空 |
| `late_fee_max` | decimal(18, 2) | Maximum fee (nullable) · 可空 |
| `overlimit_fee_basis` | tinyint | Basis: 0=ACCOUNT, 1=STATEMENT, 2=TRANSACTION (NULL=disabled) · 可空 |
| `overlimit_fee_frequency` | tinyint | Frequency: 0=ONCE_PER_STATEMENT, 1=PER_CYCLE, 2=DAILY (NULL=disabled) · 可空 |
| `overlimit_fee_apply_after_days` | int | Apply after N days (NULL=disabled) · 可空 |
| `overlimit_fee_type` | tinyint | Fee type: 0=FIXED, 1=PERCENTAGE, 2=PERCENTAGE_WITH_CAP (NULL=disabled) · 可空 |
| `overlimit_fee_value` | decimal(10, 4) | Fee amount (PRD: 100.00 AED) · 可空 |
| `overlimit_fee_min` | decimal(18, 2) | Minimum fee (nullable) · 可空 |
| `overlimit_fee_max` | decimal(18, 2) | Maximum fee (nullable) · 可空 |
| `early_settlement_percentage` | decimal(10, 4) | Early settlement fee percentage (e.g., 1.0000 for 1%) · 可空 |
| `early_settlement_min` | decimal(18, 2) | Minimum early settlement fee (nullable) · 可空 |
| `early_settlement_max` | decimal(18, 2) | Maximum early settlement fee (nullable) · 可空 |
| `vat_rate` | decimal(5, 4) | VAT rate (PRD: 0.05 for 5%) |
| `fee_rule_json` | varchar(500) | Optional extended fee rules JSON · 可空 |
| `fine_rule_json` | varchar(500) | Optional extended fine rules JSON · 可空 |
| `status` | tinyint | Version status: 0=INACTIVE, 1=ACTIVE |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |
| `processing_fee_vat_required` | tinyint | 0=not required, 1=required |
| `late_fee_vat_required` | tinyint | 0=not required, 1=required |
| `overlimit_fee_vat_required` | tinyint | 0=not required, 1=required |
| `early_settlement_vat_required` | tinyint | 0=not required, 1=required |
| `skip_statement_periods` | int | Number of statement periods to skip before first installment (0=immediate, 1=skip one month) |

## 主键 / 索引
- 主键:`id`
- `uk_product_version_code`:product_id, version_code (UNIQUE)
- `uk_product_version_no`:product_id, version_no (UNIQUE)
- `idx_product_effective`:product_id, effective_from, effective_to

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
