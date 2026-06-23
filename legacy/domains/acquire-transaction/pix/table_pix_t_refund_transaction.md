---
id: tbl_pix_t_refund_transaction
object_type: Table
domain: acquire-transaction
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:a58de775-dd0b-457d-8a31-2bfc72c081d2
tags:
- PIX
- refund
- transaction
subdomain: pix
module: transaction
sensitivity: normal
name: PIX退款交易表 t_refund_transaction
aliases:
- pix.t_refund_transaction
related_services: []
related_tables:
- tbl_pix_t_trade_transaction
- tbl_pix_t_trade_transaction_extend
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
PIX 退款交易记录表，存储 PIX 渠道下的退款交易明细，并通过 `orig_trx_voucher_no` 关联原始交易凭证号(对应 [[tbl_pix_t_trade_transaction]] 的 `trx_voucher_no`)。

## 关键列
- `trx_voucher_no` (bigint)：退款交易凭证号，主键。
- `orig_trx_voucher_no` (bigint)：原始交易凭证号，关联 [[tbl_pix_t_trade_transaction]]。
- `refund_order_type` (varchar(10))：退款订单类型。
- `transaction_amount` (decimal(19,4))：交易金额。
- `transaction_currency` (char(3))：交易币种。
- `pay_amount` (decimal(19,4))：支付金额。
- `pay_currency` (char(3))：支付币种。
- `return_profit_amount` (decimal(19,4))：退回利润金额。
- `transaction_status` (varchar(10))：交易状态。
- `trade_request_no` (bigint)：交易请求号。

## 主键/索引
- 主键：`trx_voucher_no`
- 外键关系(逻辑)：`orig_trx_voucher_no` → `pix.t_trade_transaction.trx_voucher_no`

## 校验点(QA 关注)
- `orig_trx_voucher_no` 必须能在 [[tbl_pix_t_trade_transaction]] 中找到对应原始交易记录。
- 退款的 `transaction_currency` / `pay_currency` 与原始交易币种一致性。
- `transaction_amount`、`pay_amount` 不应超过原始交易对应金额(部分退款累计校验)。
- `return_profit_amount` 与原始交易的 `profit_amount` 的对应关系。
- `transaction_status` 状态机流转是否正确。
- `trade_request_no` 的唯一性与幂等。
