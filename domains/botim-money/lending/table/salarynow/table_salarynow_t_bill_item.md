---
id: tbl_salarynow_t_bill_item
object_type: Table
name: Bill line items with flexible references to different charge types (t_bill_item)
aliases: [t_bill_item, salarynow.t_bill_item]
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

# Bill line items with flexible references to different charge types (t_bill_item)

## 用途
物理表 `salarynow.t_bill_item`,主键 `id`。Bill line items with flexible references to different charge types。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `bill_id` | bigint | Reference to t_loan_bill.id |
| `loan_id` | bigint | Reference to t_loan.id for data integrity |
| `item_type` | varchar(32) | Type of bill item: INSTALLMENT, PROCESSING_FEE, LATE_FEE, PENALTY, VAT |
| `item_id` | bigint | Reference to specific item (repayment_id, fee_id, etc.) · 可空 |
| `item_amount` | decimal(10, 2) | Amount for this bill item |
| `paid_amount` | decimal(10, 2) | Amount paid so far towards this bill item |
| `paid_at` | timestamp | Timestamp when fully paid · 可空 |
| `created_at` | timestamp | Creation timestamp |
| `updated_at` | timestamp | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `idx_bill_item_bill_id`:bill_id
- `idx_bill_item_item_id`:item_id
- `idx_bill_item_loan_id`:loan_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
