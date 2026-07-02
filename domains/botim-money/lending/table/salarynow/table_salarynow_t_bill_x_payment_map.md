---
id: tbl_salarynow_t_bill_x_payment_map
object_type: Table
name: Many-to-many mapping between bills and payments for flexible allocation (t_bill_x_payment_map)
aliases: [t_bill_x_payment_map, salarynow.t_bill_x_payment_map]
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

# Many-to-many mapping between bills and payments for flexible allocation (t_bill_x_payment_map)

## 用途
物理表 `salarynow.t_bill_x_payment_map`,主键 `id`。Many-to-many mapping between bills and payments for flexible allocation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `bill_id` | bigint | Reference to t_loan_bill.id |
| `payment_id` | bigint | Reference to t_loan_payment.id |
| `paid_to_this_bill` | decimal(10, 2) | Amount of payment allocated to this specific bill |
| `created_at` | timestamp | Creation timestamp |
| `updated_at` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uq_bill_payment_map`:bill_id, payment_id (UNIQUE)
- `idx_bill_payment_map_payment_id`:payment_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
