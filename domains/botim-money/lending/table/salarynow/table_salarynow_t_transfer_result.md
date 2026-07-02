---
id: tbl_salarynow_t_transfer_result
object_type: Table
name: Stores transfer result callback data (t_transfer_result)
aliases: [t_transfer_result, salarynow.t_transfer_result]
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

# Stores transfer result callback data (t_transfer_result)

## 用途
物理表 `salarynow.t_transfer_result`,主键 `id`。Stores transfer result callback data。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `merchant_order_no` | varchar(64) | Merchant order number |
| `payby_order_no` | varchar(64) | payby generated order number |
| `status` | varchar(32) | Status of the transfer (e.g., SUCCESS, FAILED, PENDING) |
| `beneficiary_identity` | varchar(128) | Beneficiary unique identifier |
| `beneficiary_identity_type` | varchar(32) | Type of beneficiary identity (e.g., MEMBER_ID, ACCOUNT_NO) |
| `amount` | decimal(12, 2) | Transaction amount |
| `currency` | varchar(8) | Currency code (e.g., AED) |
| `request_time` | timestamp | Request time of the transaction · 可空 |
| `created_at` | timestamp | Record creation time |
| `updated_at` | timestamp | Last update time |

## 主键 / 索引
- 主键:`id`
- `uq_transfer_result_merchant_payby_status`:merchant_order_no, payby_order_no, status (UNIQUE)
- `idx_order_no`:payby_order_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
