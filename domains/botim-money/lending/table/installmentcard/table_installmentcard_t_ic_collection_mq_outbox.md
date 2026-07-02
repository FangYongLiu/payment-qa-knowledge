---
id: tbl_installmentcard_t_ic_collection_mq_outbox
object_type: Table
name: Collection (CRM) MQ outbox (t_ic_collection_mq_outbox)
aliases: [t_ic_collection_mq_outbox, installmentcard.t_ic_collection_mq_outbox]
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

# Collection (CRM) MQ outbox (t_ic_collection_mq_outbox)

## 用途
物理表 `installmentcard.t_ic_collection_mq_outbox`,主键 `id`。Collection (CRM) MQ outbox。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `member_id` | varchar(20) | Member id · 可空 |
| `account_id` | bigint | Account id |
| `statement_id` | bigint | Statement id = collection orderNo |
| `event_type` | tinyint | 1=LOAN, 2=REPAY |
| `payment_id` | bigint | Repay events only · 可空 |
| `source` | varchar(32) | Spec source code (EARLY_SETTLEMENT=90, REFUND_RECEIPT=-1, ...) · 可空 |
| `payload` | varchar(1024) | Exact message published (point-in-time snapshot) |
| `idempotency_key` | varchar(128) | Dedupe + downstream idempotency |
| `status` | tinyint | 0=PENDING, 1=SENT, 2=FAILED |
| `retry_count` | int | Number of failed publish attempts. Flips status to FAILED once it reaches MAX_RETRY (3) in CollectionMqOutboxPublisher. |
| `last_error` | varchar(512) | Last publish failure message (exception summary, truncated to 500 chars). NULL while PENDING or SENT. · 可空 |
| `created_at` | datetime(3) | Row insertion time = business event time (millisecond precision). Set by DB default; never modified by app. |
| `sent_at` | datetime(3) | Wall-clock time the row was successfully published to RabbitMQ. NULL until status flips to SENT. · 可空 |
| `updated_at` | datetime(3) | Auto-maintained on every UPDATE; useful for "rows that have not moved recently" diagnostics. |

## 主键 / 索引
- 主键:`id`
- `uk_collection_mq_idempotency`:idempotency_key (UNIQUE)
- `idx_statement_event`:statement_id, event_type
- `idx_status_id`:status, updated_at

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
