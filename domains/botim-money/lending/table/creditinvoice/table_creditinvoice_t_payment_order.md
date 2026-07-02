---
id: tbl_creditinvoice_t_payment_order
object_type: Table
name: Generic payment order (t_payment_order)
aliases: [t_payment_order, creditinvoice.t_payment_order]
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

# Generic payment order (t_payment_order)

## 用途
物理表 `creditinvoice.t_payment_order`,主键 `id`。Generic payment order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | 待补 · 可空 |
| `payment_no` | varchar(64) | PAY-YYYYMMDDHHmmss-{6 digits} |
| `member_id` | varchar(20) | member id |
| `eid` | varchar(64) | UES ticket (non-plaintext); base user data · 可空 |
| `eid_hash` | varchar(64) | SHA-256(eid_plain + EidHashUtil.SALT); query-latest-by-eid dimension · 可空 |
| `biz_type` | varchar(32) | LIABILITY_LETTER etc. |
| `biz_ref_no` | varchar(64) | letter.request_no |
| `amount` | decimal(12, 2) | payment amount |
| `currency` | varchar(8) | currency, default AED |
| `subject` | varchar(128) | Payment subject · 可空 |
| `payment_status` | varchar(16) | INIT/SUCCESS/FAILED/TIMEOUT |
| `h5_url` | varchar(1024) | PayBy H5 redirect URL · 可空 |
| `acquire_global_id` | varchar(64) | PayBy acquire global order id · 可空 |
| `notify_msg` | varchar(4000) | Truncated to 3900 in service layer · 可空 |
| `notify_count` | int | MQ callback / notify count |
| `last_notify_time` | timestamp | Last notify time · 可空 |
| `paid_time` | timestamp | PayBy actual paid time · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_acquire_global_id`:acquire_global_id (UNIQUE)
- `uk_payment_no`:payment_no (UNIQUE)
- `idx_biz_ref_no`:biz_ref_no
- `idx_eid`:eid
- `idx_eid_hash`:eid_hash
- `idx_member_id`:member_id
- `idx_status_notify`:payment_status, last_notify_time
- `idx_status_paid_time`:payment_status, paid_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
