---
id: tbl_ecollect_t_bill_outbox
object_type: Table
name: Bill data sync outbox (t_bill_outbox)
aliases: [t_bill_outbox, ecollect.t_bill_outbox]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ecollect schema DDL
tags: [wallet, ecollect]
sensitivity: normal
related_services: []
---

# Bill data sync outbox (t_bill_outbox)

## 用途
物理表 `ecollect.t_bill_outbox`,主键 `payment_id`。Bill data sync outbox。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `payment_id` | bigint | PK; t_payment.id |
| `status` | varchar(16) | PENDING / SENT / DEAD |
| `retry_count` | int | Send attempts so far |
| `last_error` | varchar(512) | Most recent error message (truncated) · 可空 |
| `next_retry_at` | datetime | Earliest next retry (UTC) |
| `created_at` | datetime | Creation time (UTC) |
| `updated_at` | datetime | Last update time (UTC) |

## 主键 / 索引
- 主键:`payment_id`
- `idx_status_next_retry`:status, next_retry_at

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
