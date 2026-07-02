---
id: tbl_sme_t_repay_record
object_type: Table
name: Repayment history (t_repay_record)
aliases: [t_repay_record, sme.t_repay_record]
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

# Repayment history (t_repay_record)

## 用途
物理表 `sme.t_repay_record`,主键 `id`。Repayment history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `repay_no` | varchar(64) | Repayment order number |
| `repay_way` | smallint | 待补 |
| `repay_amount` | decimal(15, 2) | The amount repaid by the user |
| `currency` | char(3) | 待补 |
| `payer` | varchar(32) | Payer: The value can be user, card B merchant id, card D merchant id, or null · 可空 |
| `first_payee` | varchar(32) | First recipient |
| `sec_payee` | varchar(32) | Second recipient |
| `amount_to_sec_payee` | decimal(15, 2) | The amount of the allotment to the second payee |
| `amount_to_first_payee` | decimal(15, 2) | Money that the user pays back to first_payee = loan_amount - amount_to_sec_payee |
| `pay_channel_fee` | decimal(15, 2) | This is more than the payment fee collected · 可空 |
| `start_time` | timestamp | Time to initiate repayment |
| `payment_success_time` | timestamp | Time to receive a payby payment success notification · 可空 |
| `payment_no` | varchar(64) | The payment order number returned by payby · 可空 |
| `finish_time` | timestamp | End time · 可空 |
| `status` | smallint | Status 0: Initial status, payby is not submitted, 1: payby is submitted, 2: repayment is successful, 3: verification is complete, -2: repayment failed |
| `ref_no` | varchar(50) | 待补 · 可空 |
| `When` | repay | 待补 · 可空 |
| `repay_success_time` | timestamp | The time of successful repayment · 可空 |
| `loan_order_no` | varchar(64) | order_no in table t_loan_order |
| `third_user_id` | varchar(20) | Third-party channel user id |
| `third_party_name` | varchar(20) | Order source channel name |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Modification time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
