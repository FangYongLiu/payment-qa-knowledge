---
id: tbl_loyalty_t_batch_cashback_records
object_type: Table
name: Individual records from batch cashback uploads (t_batch_cashback_records)
aliases: [t_batch_cashback_records, loyalty.t_batch_cashback_records]
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

# Individual records from batch cashback uploads (t_batch_cashback_records)

## 用途
物理表 `loyalty.t_batch_cashback_records`,主键 `id`。Individual records from batch cashback uploads。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key · 可空 |
| `job_id` | varchar(36) | FK to t_batch_cashback_jobs.job_id |
| `row_no` | int unsigned | 1-based row number in CSV |
| `ucid` | varchar(50) | User UCID |
| `amount` | decimal(15, 2) | Cashback amount |
| `description` | varchar(200) | Optional description from CSV · 可空 |
| `currency` | varchar(3) | 待补 |
| `status` | varchar(15) | pending|processing|success|failed |
| `m2u_request_id` | varchar(100) | Idempotency key: BCR_{job_id_short}_{row} · 可空 |
| `m2u_order_no` | varchar(100) | PayBy order number · 可空 |
| `m2u_status` | varchar(50) | Raw status from M2U API · 可空 |
| `error_code` | varchar(50) | Error code if failed · 可空 |
| `error_message` | varchar(500) | Error message if failed · 可空 |
| `processed_at` | timestamp | When this record was processed · 可空 |
| `created_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_batch_cashback_records_request`:m2u_request_id (UNIQUE)
- `idx_batch_cashback_records_job`:job_id, row_no
- `idx_batch_cashback_records_ucid`:ucid
- `idx_batch_cashback_records_ucid_status`:ucid, status

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
