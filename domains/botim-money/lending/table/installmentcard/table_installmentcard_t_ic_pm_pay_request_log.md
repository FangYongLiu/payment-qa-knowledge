---
id: tbl_installmentcard_t_ic_pm_pay_request_log
object_type: Table
name: Payment request log: tracks manual and CRS payment requests (t_ic_pm_pay_request_log)
aliases: [t_ic_pm_pay_request_log, installmentcard.t_ic_pm_pay_request_log]
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

# Payment request log: tracks manual and CRS payment requests (t_ic_pm_pay_request_log)

## 用途
物理表 `installmentcard.t_ic_pm_pay_request_log`,主键 `id`。Payment request log: tracks manual and CRS payment requests。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK · 可空 |
| `voucher_no` | varchar(64) | Manual: generated before payment. CRS: from CRS callback · 可空 |
| `member_id` | varchar(32) | Member identifier |
| `request_amount` | decimal(18, 2) | Requested payment amount |
| `paid_amount` | decimal(18, 2) | Actual paid amount (populated on callback) · 可空 |
| `status` | tinyint | 0=CREATED, 1=CRS_CALL_FAIL, 2=PENDING, 3=PARTIAL, 4=SUCCESS, 5=FAILED, 6=SETTLED, 7=CANCELLED |
| `type` | tinyint | 0=MANUAL, 1=CRS |
| `payment_channel` | varchar(128) | Payment channel info (manual only, populated from callback) · 可空 |
| `paid_at` | datetime(3) | Actual payment time from provider · 可空 |
| `last_provider_status` | varchar(64) | Last status received from provider callback · 可空 |
| `created_at` | datetime(3) | Record creation time |
| `updated_at` | datetime(3) | Last update time |
| `settlement_id` | varchar(64) | Settlement-estimate snapshot id returned by /repayment-pay-summary; ties this request to the chosen pay-mode estimate (and to the loan/statement scope captured on the snapshot) · 可空 |
| `pay_mode` | tinyint | Selected pay mode. 0=STATEMENT, 1=STATEMENT_PARTIAL, 2=PAY_ALL, 3=SETTLE_LOAN. NULL on legacy CRS rows · 可空 |
| `card_type` | varchar(32) | Card type captured from gateway when payment lands (e.g., DEBIT, CREDIT) · 可空 |
| `card_last4` | varchar(8) | Last 4 digits of the card used for payment (audit/UX only) · 可空 |
| `version` | int | Optimistic-lock counter for status transitions |
| `status_polled_at` | datetime(3) | First /payment/status call against this row while still PENDING. The init decision table reads this to distinguish "user finished SDK gracefully, MQ lagging" from "user abandoned the page" when Tradeii reports W · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id
- `idx_settlement_member`:settlement_id, member_id
- `idx_voucher_no`:voucher_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
