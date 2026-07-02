---
id: tbl_rnpl_t_payment
object_type: Table
name: Table to store payment details (t_payment)
aliases: [t_payment, rnpl.t_payment]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Table to store payment details (t_payment)

## 用途
物理表 `rnpl.t_payment`,主键 `payment_id`。Table to store payment details。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `payment_id` | int | Primary key, auto-increment · 可空 |
| `payment_order_no` | varchar(64) | Payment order number |
| `payment_ref_no` | varchar(32) | Payment reference number · 可空 |
| `payment_type` | tinyint | Payment type 1 for dd offline, 2 payBy |
| `payment_time` | timestamp | Time for the payment · 可空 |
| `total_amount` | decimal(10, 2) | The total amount paid |
| `currency` | char(3) | Currency, default AED |
| `utilized_amount` | decimal(10, 2) | The total amount paid for this EMI · 可空 |
| `remaining_amount` | decimal(10, 2) | The remaining amount to be paid for this EMI · 可空 |
| `payment_status` | tinyint | Payment status: -1 failed, 0 waiting, 1 success |
| `returned_record_id` | int | Return record ID · 可空 |
| `contract_id` | int | Use for the bill and contract association · 可空 |
| `payment_channel` | varchar(64) | Payment channel like botim or direct debit · 可空 |
| `updated_time` | timestamp | The last payment update date of the EMI · 可空 |
| `created_time` | timestamp | Created date · 可空 |
| `comments` | varchar(256) | payment comments · 可空 |
| `is_settled` | tinyint | 0: if payment is fully utilized, else 1 |
| `dds_ref_no` | varchar(64) | direct debit reference number · 可空 |

## 主键 / 索引
- 主键:`payment_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
