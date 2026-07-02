---
id: tbl_installmentcard_t_ic_ntf_notification_log
object_type: Table
name: t_ic_ntf_notification_log (t_ic_ntf_notification_log)
aliases: [t_ic_ntf_notification_log, installmentcard.t_ic_ntf_notification_log]
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

# t_ic_ntf_notification_log (t_ic_ntf_notification_log)

## 用途
物理表 `installmentcard.t_ic_ntf_notification_log`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `member_id` | varchar(32) | External member/customer identifier the notification is addressed to |
| `account_id` | bigint | Installment card account id (FK to t_ic_am_account.id, no SQL-level constraint) |
| `notification_type` | tinyint | Notification type as integer enum (TINYINT). Example mapping: 1=PAYMENT_REMINDER, 2=OVERDUE_REMINDER, 3=ACTIVATION, 4=LOAN_CREATION, 5=STATEMENT_GENERATION, 6=REFUND_LOAN_OUTSTANDING, 7=REFUND_LOAN_CLOSED, 8=REFUND_LOAN_CLOSED_WALLET_CREDIT, 9=TRANSACTION_REJECTION |
| `ref_type` | tinyint | Referenced entity type as integer enum (TINYINT). Example mapping: 1=STATEMENT, 2=LOAN, 3=CARD_TXN, 4=ACCOUNT. Null when the notification is not scoped to a specific business object · 可空 |
| `ref_id` | bigint | Id of the referenced entity (interpretation depends on ref_type) · 可空 |
| `variant` | varchar(32) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_member`:member_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
