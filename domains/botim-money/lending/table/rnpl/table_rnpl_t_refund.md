---
id: tbl_rnpl_t_refund
object_type: Table
name: Table to store refund details (t_refund)
aliases: [t_refund, rnpl.t_refund]
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

# Table to store refund details (t_refund)

## 用途
物理表 `rnpl.t_refund`,主键 `refund_id`。Table to store refund details。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `refund_id` | int | Primary key, auto-increment · 可空 |
| `payment_id` | int | Foreign key to the payment.payment_id. Links the refund to the original payment |
| `refund_order_no` | varchar(64) | Refund order number |
| `refund_ref_no` | varchar(32) | Refund reference number · 可空 |
| `refund_amount` | decimal(10, 2) | The refunded amount |
| `refund_time` | timestamp | The date when the refund was processed · 可空 |
| `refund_reason` | varchar(255) | Reason for the refund (optional) · 可空 |
| `created_time` | timestamp | Timestamp when the refund record was created · 可空 |
| `refund_status` | tinyint | Refund status: 0 for initiated, 1 for completed, -1 for failed |

## 主键 / 索引
- 主键:`refund_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
