---
id: tbl_npss_t_qr_refund_order
object_type: Table
name: qr refund order (t_qr_refund_order)
aliases: [t_qr_refund_order, npss.t_qr_refund_order]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# qr refund order (t_qr_refund_order)

## 用途
物理表 `npss.t_qr_refund_order`,主键 `qr_refund_order_id`。qr refund order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `qr_refund_order_id` | bigint(19) | qr refund order id |
| `qr_order_id` | bigint(19) | qr order id |
| `merchant_id` | varchar(20) | merchant id |
| `amount` | decimal(19, 4) | amount |
| `currency` | char(3) | currency |
| `reference_no` | varchar(32) | reference no, inst_order_no |
| `refund_times` | int(15) | refund times |
| `payment_id` | bigint(19) | Payment Id · 可空 |
| `id_sct` | varchar(32) | channel id sct · 可空 |
| `status` | char | status, I- Initial, F-Fail,S-Success,R-Refund |
| `reason` | varchar(32) | reason · 可空 |
| `result_phase` | varchar(10) | result phase, vp-verifyPayment,cp-confirmPayment,qr-requestToPay · 可空 |
| `result_code` | varchar(32) | result code · 可空 |
| `extension` | varchar(255) | extension · 可空 |
| `gmt_create` | timestamp | create time |
| `gmt_modified` | timestamp | modify time · 可空 |
| `gmt_finished` | timestamp | finish time · 可空 |

## 主键 / 索引
- 主键:`qr_refund_order_id`
- `uk_qr_rft_reference_no`:reference_no (UNIQUE)
- `idx_qr_rft_id_sct`:id_sct

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
