---
id: tbl_installmentcard_t_ic_stl_overpayment_credit_usage
object_type: Table
name: Maps payment to funding sources (e.g., account credit) (t_ic_stl_overpayment_credit_usage)
aliases: [t_ic_stl_overpayment_credit_usage, installmentcard.t_ic_stl_overpayment_credit_usage]
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

# Maps payment to funding sources (e.g., account credit) (t_ic_stl_overpayment_credit_usage)

## 用途
物理表 `installmentcard.t_ic_stl_overpayment_credit_usage`,主键 `id`。Maps payment to funding sources (e.g., account credit)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `payment_id` | bigint | Logical ref to t_ic_stl_payment.id (no FK) |
| `source_type` | tinyint | Funding source type: 0=CREDIT |
| `source_id` | bigint | Source record id. For CREDIT: logical ref to t_ic_stl_overpayment_credit.id (no FK) |
| `used_amount` | decimal(18, 2) | Amount consumed from source for this payment |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_payment_id`:payment_id
- `idx_source`:source_id, source_type

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
