---
id: tbl_installmentcard_t_ic_cm_txn_event
object_type: Table
name: Immutable gateway transaction events for replay, debugging, and idempotency (t_ic_cm_txn_event)
aliases: [t_ic_cm_txn_event, installmentcard.t_ic_cm_txn_event]
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

# Immutable gateway transaction events for replay, debugging, and idempotency (t_ic_cm_txn_event)

## 用途
物理表 `installmentcard.t_ic_cm_txn_event`,主键 `id`。Immutable gateway transaction events for replay, debugging, and idempotency。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `trx_voucher_no` | varchar(64) | PPC transaction voucher number (extracted for easier querying) · 可空 |
| `request_id` | varchar(64) | Client/request correlation ID for idempotency and end-to-end tracing (e.g., activation or posting requestId) · 可空 |
| `event_type` | tinyint | Event type: 0=AUTH, 1=CAPTURE, 2=REVERSAL, 3=REFUND, 4=RELEASE, 5=FORCE_SETTLEMENT, 6=CHARGEBACK |
| `ppc_txn_type` | varchar(10) | PPC transaction type: T, TC, S, FS, R, RL, CB, BR, F, RF · 可空 |
| `event_time` | datetime | Event time as per gateway |
| `payload` | varchar(1024) | Raw event payload (JSON text) |
| `processed_status` | tinyint | Processing status: 0=NEW, 1=PROCESSED, 2=FAILED |
| `processed_at` | datetime | When event was processed (success or failure) · 可空 |
| `received_at` | datetime | System receive time (when our service received event) |
| `error_message` | varchar(500) | Error message if processing failed · 可空 |
| `created_at` | datetime | Record creation timestamp |
| `updated_at` | datetime | Last update timestamp |

## 主键 / 索引
- 主键:`id`
- `uk_txn_event_request_id`:request_id (UNIQUE)
- `idx_event_time`:event_time
- `idx_trx_voucher_no`:trx_voucher_no

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
