---
id: tbl_botimsnpl_t_sl_transfer_info
object_type: Table
name: SNPL Transaction & Beneficiary Combined Information Table (t_sl_transfer_info)
aliases: [t_sl_transfer_info, botimsnpl.t_sl_transfer_info]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# SNPL Transaction & Beneficiary Combined Information Table (t_sl_transfer_info)

## 用途
物理表 `botimsnpl.t_sl_transfer_info`,主键 `id`。SNPL Transaction & Beneficiary Combined Information Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key ID · 可空 |
| `uid` | varchar(32) | risk application_id |
| `order_no` | varchar(32) | Order number (unique) |
| `user_id` | varchar(20) | user id |
| `identity` | varchar(50) | identity |
| `beneficiary_id` | varchar(64) | Unique identifier of beneficiary |
| `order_amount` | decimal(16, 2) | Order amount (INR) |
| `transfer_type` | varchar(16) | Transfer type (BANK/WALLET/UPI) |
| `beneficiary_full_name` | varchar(128) | Beneficiary full name (English) · 可空 |
| `beneficiary_mobile_number` | varchar(20) | Beneficiary mobile number · 可空 |
| `bank_name` | varchar(128) | Bank name · 可空 |
| `bank_account_number` | varchar(64) | Bank account number (desensitized storage) · 可空 |
| `ifsc_code` | varchar(32) | Bank IFSC code (India specific) · 可空 |
| `wallet_name` | varchar(64) | Wallet name (e.g., Paytm/PhonePe) · 可空 |
| `wallet_id` | varchar(64) | Wallet account ID · 可空 |
| `upi_id` | varchar(64) | UPI ID (Unified Payments Interface, India) · 可空 |
| `create_time` | timestamp | Order creation time |
| `paid_time` | timestamp | Payment completion time · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_uid`:uid (UNIQUE)
- `idx_beneficiary_full_Name`:beneficiary_full_name
- `idx_beneficiary_id`:beneficiary_id
- `idx_beneficiary_mobile`:beneficiary_mobile_number
- `idx_create_time`:create_time
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
