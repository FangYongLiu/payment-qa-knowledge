---
id: tbl_loyalty_t_batch_gold_records
object_type: Table
name: Individual records from batch gold/silver uploads (t_batch_gold_records)
aliases: [t_batch_gold_records, loyalty.t_batch_gold_records]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: loyalty schema DDL
tags: [marketing, loyalty]
sensitivity: normal
related_services: []
---

# Individual records from batch gold/silver uploads (t_batch_gold_records)

## 用途
物理表 `loyalty.t_batch_gold_records`,主键 `id`。Individual records from batch gold/silver uploads。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key · 可空 |
| `job_id` | varchar(36) | FK to t_batch_gold_jobs.job_id |
| `row_no` | int unsigned | 1-based row number in CSV |
| `ucid` | varchar(50) | User UCID (after integration_id resolution) |
| `asset` | varchar(10) | gold | silver (per-row) |
| `mode` | varchar(10) | aed | grams (denomination unit) |
| `amount` | decimal(18, 8) | Amount denominated by mode (AED uses 2dp in practice, grams up to 8dp) |
| `description` | varchar(200) | Optional description from CSV · 可空 |
| `status` | varchar(20) | pending|processing|success|waiting|cashback_issued|not_rewarded|failed |
| `request_order_no` | varchar(100) | Idempotency key sent to Gold Service: LOYALTY_GOLD_*/LOYALTY_SILVER_* · 可空 |
| `gold_reward_transaction_id` | bigint unsigned | FK to t_gold_reward_transactions_*.id once inserted · 可空 |
| `gold_service_status` | varchar(50) | Raw status from Gold Service airdrop response · 可空 |
| `error_code` | varchar(50) | Error code if failed · 可空 |
| `error_message` | varchar(500) | Error message if failed · 可空 |
| `processed_at` | timestamp | When this record reached a terminal state · 可空 |
| `created_at` | timestamp | Record creation time |

## 主键 / 索引
- 主键:`id`
- `uk_batch_gold_records_request`:request_order_no (UNIQUE)
- `idx_batch_gold_records_job`:job_id, row_no
- `idx_batch_gold_records_ucid`:ucid

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
