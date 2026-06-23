---
id: tbl_pix_trade_transaction
object_type: Table
domain: acquire-transaction
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:4538bf84-a043-4d3d-a9fd-d0fcbb9bc671
tags:
- PIX
- 交易表
subdomain: null
module: null
sensitivity: normal
name: PIX交易表 t_trade_transaction
aliases:
- pix.t_trade_transaction
related_services: []
related_tables:
- tbl_pix_refund_transaction
- tbl_pix_trade_relate_order
- tbl_pix_trade_transaction_extend
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
PIX schema 下的核心交易记录表 `pix.t_trade_transaction`，存储 PIX 收单交易的主体信息，包括交易金额、币种、汇率/保证金版本、利润、渠道及交易状态等。

## 关键列
- `trx_voucher_no` (bigint, PK)：交易凭证号，主键。
- `channel_code` (varchar 32)：渠道编码。
- `order_type` (varchar 32)：订单类型。
- `member_id` (varchar 20)：会员 ID。
- `transaction_amount` (decimal 19,4)：交易金额。
- `transaction_currency` (char 3)：交易币种。
- `pay_amount` (decimal 19,4)：支付金额。
- `pay_currency` (char 3)：支付币种。
- `rate_version` (bigint)：汇率版本。
- `margin_version` (bigint)：保证金版本。
- `profit_amount` (decimal 19,4)：利润金额。
- `transaction_status` (varchar 10)：交易状态。
- `unity_result_code` (varchar 50)：统一结果码。
- `channel_result_code` (varchar 50)：渠道结果码。
- `paid_time` (timestamp 3)：支付完成时间。

## 主键/索引
- 主键：`trx_voucher_no`。

## 校验点(QA 关注)
- `trx_voucher_no` 唯一性，作为关联 `t_refund_transaction.orig_trx_voucher_no` 与 `t_trade_relate_order.trx_voucher_no` 的主键。
- 金额/币种字段一致性：`transaction_amount`/`transaction_currency` 与 `pay_amount`/`pay_currency` 在跨币种场景下需结合 `rate_version`、`margin_version` 校验。
- `transaction_status` 的状态流转与 `unity_result_code`、`channel_result_code` 的对应关系。
- `paid_time` 仅在支付成功后写入，需与 `transaction_status` 一致。
- `channel_code`、`order_type`、`member_id` 等关键维度字段是否完整记录。
