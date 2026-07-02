---
id: tbl_rnpl_t_bill_v2
object_type: Table
name: t_bill_v2 (t_bill_v2)
aliases: [t_bill_v2, rnpl.t_bill_v2]
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

# t_bill_v2 (t_bill_v2)

## 用途
物理表 `rnpl.t_bill_v2`,主键 `bill_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `bill_id` | int | Primary key, auto-increment · 可空 |
| `bill_sequence` | tinyint | Use for the bill seq number |
| `period_no` | tinyint | Use for the bill period number · 可空 |
| `loan_id` | int | Use for the bill loan association |
| `loan_order_no` | varchar(64) | Use for the bill loan association by order number |
| `contract_id` | int | Use for the bill and contract association · 可空 |
| `user_id` | varchar(32) | Use for the bill and user association · 可空 |
| `due_time` | timestamp | The due date of the EMI |
| `bill_type` | tinyint | dp :0, rp: 1 |
| `currency` | char(3) | Bill currency |
| `principal` | decimal(10, 2) | Principal amount |
| `instalment_fee` | decimal(10, 2) | Interest for the current bill if rp · 可空 |
| `handling_fee` | decimal(10, 2) | Handling fees if dp · 可空 |
| `bill_amount` | decimal(10, 2) | The total amount for this EMI |
| `total_paid` | decimal(10, 2) | The total amount paid for this EMI · 可空 |
| `remaining_amount` | decimal(10, 2) | The remaining amount to be paid for this EMI · 可空 |
| `fine_amount` | decimal(10, 2) | The fine amount applied to the overdue EMI · 可空 |
| `fine_waived` | tinyint | 1: fine has been waived off, 0: not waived off · 可空 |
| `bill_status` | tinyint | Status: 1: pending; 2 cleared; -1: canceled (overdue first bill order canceled) · 可空 |
| `payment_settled_date` | timestamp | The payment finish date of the EMI · 可空 |
| `updated_time` | timestamp | The last update date for the EMI · 可空 |
| `created_time` | timestamp | created time · 可空 |

## 主键 / 索引
- 主键:`bill_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
