---
id: tbl_installmentcard_t_ic_pgw_refund_transfer
object_type: Table
name: Last update time (t_ic_pgw_refund_transfer)
aliases: [t_ic_pgw_refund_transfer, installmentcard.t_ic_pgw_refund_transfer]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: installmentcard schema DDL
tags: [lending, installmentcard]
sensitivity: normal
related_services: []
---

# Last update time (t_ic_pgw_refund_transfer)

## 用途
物理表 `installmentcard.t_ic_pgw_refund_transfer`,主键 `id`。Last update time。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK · 可空 |
| `merchant_order_no` | varchar(64) | Our merchant order number — idempotency key for the placeTransferOrder call |
| `payby_order_no` | varchar(64) | PayBy-assigned orderNo returned by placeTransferOrder · 可空 |
| `member_id` | varchar(32) | Beneficiary member identifier (recipient of the wallet transfer) |
| `ref_id` | bigint | Reference id; semantic depends on paymt_origin (logical ref to refund txn id or pay_request_log.id, no FK) |
| `paymt_origin` | tinyint | PaymentOrigin enum: 0=REFUND, 1=PAYMENT |
| `amount` | decimal(18, 2) | Refund amount in AED |
| `status` | tinyint | 0=PENDING, 1=SUCCESS, 2=FAILURE (RefundTransferStatus enum) |
| `executed_at` | datetime(3) | When PayBy confirmed the transfer (set on SUCCESS) · 可空 |
| `version` | int | Optimistic-lock counter for status transitions |
| `created_at` | datetime(3) | Record creation time |
| `updated_at` | datetime(3) | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id
- `idx_payby_order_no`:payby_order_no
- `idx_ref_id_paymt_origin`:ref_id, paymt_origin

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
