---
id: tbl_creditinvoice_t_liability_letter
object_type: Table
name: Liability/No-Liability Letter application (t_liability_letter)
aliases: [t_liability_letter, creditinvoice.t_liability_letter]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditinvoice schema DDL
tags: [lending, creditinvoice]
sensitivity: normal
related_services: []
---

# Liability/No-Liability Letter application (t_liability_letter)

## 用途
物理表 `creditinvoice.t_liability_letter`,主键 `id`。Liability/No-Liability Letter application。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key · 可空 |
| `request_no` | varchar(32) | request no |
| `member_id` | varchar(20) | user id |
| `phone` | varchar(20) | encrypted phone number |
| `eid` | varchar(64) | encrypted eid |
| `eid_hash` | varchar(64) | SHA-256(eid_plain + EidHashUtil.SALT), 30-day dedup dimension |
| `full_name` | varchar(128) | encrypted full name |
| `email` | varchar(128) | Recipient email |
| `letter_type` | varchar(32) | LIABILITY / NO_LIABILITY |
| `address_to` | varchar(128) | Personal / Others / bank name |
| `payment_no` | varchar(64) | Linked payment_no; NULL for manual-replace (no charge) · 可空 |
| `letter_status` | varchar(16) | WAIT_PAY/UNDER_PROCESS/GENERATED/COMPLETED/REJECTED/CLOSED |
| `terminal_reason` | varchar(64) | REJECTED: DUPLICATE_EID_VALID_LETTER/LETTER_TYPE_MISMATCH/OTHER; CLOSED: LETTER_REPLACED/PAYMENT_FAILED · 可空 |
| `loan_snapshot` | mediumtext | JSON snapshot of 3-product loan query result · 可空 |
| `qr_id` | varchar(64) | same value as t_letter_qr_code.qr_id · 可空 |
| `letter_oss_path` | varchar(512) | UFS OSS path of the Letter PDF · 可空 |
| `invoice_no` | varchar(32) | invoice no · 可空 |
| `invoice_oss_path` | varchar(512) | UFS OSS path of the Tax Invoice PDF · 可空 |
| `generated_time` | timestamp | Time the letter PDF was generated · 可空 |
| `valid_until` | timestamp | generated_time + qrcode.default-valid-days · 可空 |
| `email_sent_time` | timestamp | Time the letter email was sent · 可空 |
| `next_retry_stage` | varchar(32) | LETTER_GENERATE / EMAIL_SEND · 可空 |
| `next_retry_time` | timestamp | Next retry time; NULL means no pending retry · 可空 |
| `last_retry_time` | timestamp | Last retry attempt time · 可空 |
| `retry_count` | int | Accumulated retry count |
| `fail_reason` | varchar(1024) | Last failure reason (truncated) · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_qr_id`:qr_id (UNIQUE)
- `uk_request_no`:request_no (UNIQUE)
- `idx_eid_hash`:eid_hash
- `idx_eid_status_id`:eid_hash, letter_status, id
- `idx_member_id`:member_id
- `idx_next_retry_time`:next_retry_time
- `idx_payment_no`:payment_no
- `idx_phone`:phone

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
