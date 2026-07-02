---
id: tbl_aml_t_payment_event_wide_2025
object_type: Table
name: Payment event wide table (t_payment_event_wide_2025)
aliases: [t_payment_event_wide_2025, aml.t_payment_event_wide_2025]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: aml schema DDL
tags: [compliance, aml]
sensitivity: normal
related_services: []
---

# Payment event wide table (t_payment_event_wide_2025)

## 用途
物理表 `aml.t_payment_event_wide_2025`,主键 `id`。Payment event wide table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key · 可空 |
| `payment_order_no` | varchar(64) | Payment order number (unique) |
| `transaction_id` | varchar(64) | Transaction ID · 可空 |
| `merchant_order_no` | varchar(128) | Merchant order number · 可空 |
| `tid` | varchar(64) | Transaction identification · 可空 |
| `cis_ticket` | varchar(64) | CIS ticket · 可空 |
| `biz_product_code` | varchar(10) | Business product code · 可空 |
| `pay_channel` | varchar(32) | Payment channel · 可空 |
| `payer_member_id` | varchar(32) | Payer member ID · 可空 |
| `payee_member_id` | varchar(32) | Payee member ID · 可空 |
| `merchant_id` | varchar(32) | Merchant ID · 可空 |
| `payer_eid` | varchar(32) | Payer EID · 可空 |
| `pay_amount` | decimal(15, 4) | Payment amount · 可空 |
| `currency` | char(3) | Currency code · 可空 |
| `card_no` | varchar(30) | Card number (masked) · 可空 |
| `card_bin` | varchar(16) | Card BIN (first 6 digits) · 可空 |
| `card_last_four` | varchar(4) | Card last four digits · 可空 |
| `device_id` | varchar(128) | Device ID · 可空 |
| `ip` | varchar(64) | IP address · 可空 |
| `inst_order_no` | varchar(64) | Institution order number · 可空 |
| `arn` | varchar(32) | ARN (Acquirer Reference Number) · 可空 |
| `auth_code` | varchar(32) | Authorization code · 可空 |
| `eci` | varchar(32) | ECI (Electronic Commerce Indicator) · 可空 |
| `identity_type` | varchar(32) | Identity type · 可空 |
| `customer_event_type` | varchar(32) | Customer event type · 可空 |
| `risk_status` | varchar(32) | Risk status (PASS, REJECT, REVIEW) · 可空 |
| `reject_flag` | char | Reject flag (Y/N) · 可空 |
| `reject_source` | varchar(32) | Reject source · 可空 |
| `status` | varchar(16) | Status (PROCESS, SUCCESS, FAILED) · 可空 |
| `key_rule` | varchar(128) | Key rule codes (comma separated) · 可空 |
| `extension` | varchar(500) | Extension fields (JSON format) · 可空 |
| `event_time` | datetime | Event time (trade time) · 可空 |
| `create_time` | datetime | Create time |
| `update_time` | datetime | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_payment_order_no`:payment_order_no (UNIQUE)
- `idx_create_time`:create_time
- `idx_payer_member_id_event_time`:payer_member_id, event_time
- `idx_transaction_id`:transaction_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
