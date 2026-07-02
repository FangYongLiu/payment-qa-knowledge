---
id: tbl_salarynow_t_product
object_type: Table
name: Product definitions for loan offers, including charges and configuration (t_product)
aliases: [t_product, salarynow.t_product]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: salarynow schema DDL
tags: [lending, salarynow]
sensitivity: normal
related_services: []
---

# Product definitions for loan offers, including charges and configuration (t_product)

## 用途
物理表 `salarynow.t_product`,主键 `id`。Product definitions for loan offers, including charges and configuration。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `name` | varchar(64) | Auto-generated product name |
| `max_installments` | smallint(2) | Maximum number of repayments allowed |
| `risk_level` | varchar(20) | Risk level for the product |
| `product_type` | varchar(20) | Type of product: REGULAR or PROMOTIONAL |
| `interest_rate` | decimal(5, 2) | Interest rate (%) for this product |
| `irr_rate` | decimal(5, 2) | irr rate (%) for this product |
| `processing_fee` | decimal(10, 2) | Processing fee for the product fixed amount |
| `processing_fee_percentage` | decimal(10, 2) | Processing fee for the product in percentage |
| `processing_fee_max_cap` | decimal(10, 2) | Processing fee for the product max cap |
| `fine_charges` | decimal(10, 2) | Fine charges for late payment fixed amount |
| `fine_charges_percentage` | decimal(10, 2) | Fine charges for late payment in percentage |
| `fine_charges_max_cap` | decimal(10, 2) | Fine charges for late payment max cap |
| `vat_percentage` | decimal(5, 2) | VAT percentage |
| `grace_days` | int | number of grace period days |
| `lpf_grace_period_days` | int | Grace period days before late payment fee applies |
| `lpf_min_amount` | decimal(10, 2) | Minimum late payment fee amount |
| `lpf_max_amount` | decimal(10, 2) | Maximum late payment fee amount |
| `lpf_percentage` | decimal(10, 2) | Late payment fee percentage |
| `lpf_vat_percentage` | decimal(10, 2) | VAT percentage on late payment fee |
| `status` | varchar(20) | Product status (ACTIVE, INACTIVE, HOLD etc.) |
| `start_time` | timestamp | Product start validity time |
| `end_time` | timestamp | Product end validity time · 可空 |
| `version` | int | Version of the product |
| `created_at` | timestamp | Record creation time |
| `updated_at` | timestamp | Last update time |

## 主键 / 索引
- 主键:`id`
- `uq_product_max_installments_risk_product_type_version`:max_installments, risk_level, product_type, version (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
