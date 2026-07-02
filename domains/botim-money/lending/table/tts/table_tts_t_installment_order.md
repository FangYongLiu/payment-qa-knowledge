---
id: tbl_tts_t_installment_order
object_type: Table
name: Installment order (t_installment_order)
aliases: [t_installment_order, tts.t_installment_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tts schema DDL
tags: [lending, tts]
sensitivity: normal
related_services: []
---

# Installment order (t_installment_order)

## 用途
物理表 `tts.t_installment_order`,主键 `pay_voucher_no`。Installment order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `pay_voucher_no` | bigint(21) | pay voucher no |
| `member_id` | varchar(20) | member id · 可空 |
| `merchant_id` | varchar(20) | merchant id |
| `card_no` | varchar(32) | card_no · 可空 |
| `supplier_code` | varchar(5) | supplier: VISA/ |
| `external_reference_no` | varchar(50) | external ref no · 可空 |
| `amount` | decimal(20, 4) | amount |
| `refundable_amount` | decimal(20, 4) | remaining refundable amount · 可空 |
| `currency` | char(3) | currency |
| `installment_source` | varchar(4) | source: POS/ECOM · 可空 |
| `status` | varchar(2) | status: P-Pending,S-Success,F-Failed,RP-Refund_Process,R-Refunded,RF-Refund_Failed |
| `cancel_voucher_no` | bigint | cancel voucher no · 可空 |
| `result_code` | varchar(32) | result code · 可空 |
| `memo` | varchar(128) | memo · 可空 |
| `unity_result_code` | varchar(50) | unity result code · 可空 |
| `extension` | varchar(512) | extension · 可空 |
| `gmt_create` | timestamp(3) | create time |
| `gmt_modified` | timestamp(3) | modify time · 可空 |
| `gmt_finish` | timestamp(3) | finish time · 可空 |

## 主键 / 索引
- 主键:`pay_voucher_no`
- `uk_install_order_cancel_no`:cancel_voucher_no (UNIQUE)
- `uk_install_order_ref_no`:supplier_code, external_reference_no (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
