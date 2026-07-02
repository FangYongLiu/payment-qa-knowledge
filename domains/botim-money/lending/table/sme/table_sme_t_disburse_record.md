---
id: tbl_sme_t_disburse_record
object_type: Table
name: Loan record sheet (t_disburse_record)
aliases: [t_disburse_record, sme.t_disburse_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# Loan record sheet (t_disburse_record)

## 用途
物理表 `sme.t_disburse_record`,主键 `id`。Loan record sheet。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `disburse_no` | varchar(64) | The loan slip number sent to the payment platform |
| `due_time` | timestamp | Time of loan due |
| `submit_time` | timestamp | Submission of loan success time · 可空 |
| `finish_time` | timestamp | Loan success or failure time · 可空 |
| `refund_time` | datetime | Refund time · 可空 |
| `status` | smallint | 待补 |
| `amount` | decimal(12, 4) | Loan amount |
| `currency` | char(3) | Monetary unit |
| `payment_no` | varchar(64) | The payment order number of the payment channel · 可空 |
| `channel_fee` | decimal(10, 2) | Loan commission · 可空 |
| `beneficiary_snap_id` | int | Collection information |
| `fail_reason` | varchar(255) | Reasons for loan failure · 可空 |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
