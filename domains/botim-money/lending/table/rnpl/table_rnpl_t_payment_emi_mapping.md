---
id: tbl_rnpl_t_payment_emi_mapping
object_type: Table
name: Table to map payments to EMI bills (t_payment_emi_mapping)
aliases: [t_payment_emi_mapping, rnpl.t_payment_emi_mapping]
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

# Table to map payments to EMI bills (t_payment_emi_mapping)

## 用途
物理表 `rnpl.t_payment_emi_mapping`,主键 `mapping_id`。Table to map payments to EMI bills。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `mapping_id` | int | Primary key, auto-increment · 可空 |
| `payment_id` | int | Foreign key to Payments.payment_id |
| `bill_id` | int | Foreign key to EMIs.emi_id |
| `paid_amount` | decimal(10, 2) | Amount paid towards this specific EMI · 可空 |
| `created_time` | timestamp | created time |

## 主键 / 索引
- 主键:`mapping_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
