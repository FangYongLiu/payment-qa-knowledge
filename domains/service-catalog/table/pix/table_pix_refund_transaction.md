---
id: tbl_pix_refund_transaction
object_type: Table
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:4538bf84-a043-4d3d-a9fd-d0fcbb9bc671
tags:
- PIX
- refund
- transaction
subdomain: null
module: null
sensitivity: normal
name: PIX退款交易表 t_refund_transaction
aliases:
- pix.t_refund_transaction
related_services:
- svc_pix
---

## 用途
PIX schema 下的退款交易表，记录 PIX 渠道的退款交易记录，并通过 `orig_trx_voucher_no` 关联原始交易（`t_trade_transaction.trx_voucher_no`）。

## 关键列
- `trx_voucher_no` (bigint) — 主键，退款交易的凭证号
- `orig_trx_voucher_no` (bigint) — 原交易凭证号，关联 `t_trade_transaction.trx_voucher_no`
- `refund_order_type` (varchar 10) — 退款订单类型
- `transaction_amount` (decimal 19,4) — 交易金额
- `transaction_currency` (char 3) — 交易币种
- `pay_amount` (decimal 19,4) — 支付金额
- `pay_currency` (char 3) — 支付币种
- `return_profit_amount` (decimal 19,4) — 退还利润金额
- `transaction_status` (varchar 10) — 交易状态
- `trade_request_no` (bigint) — 交易请求号，关联 `t_trade_relate_order.trade_request_no`
- （原图字段被截断，可能存在更多字段）

## 主键/索引
- 主键：`trx_voucher_no`
- 关联键：
  - `orig_trx_voucher_no` → `t_trade_transaction.trx_voucher_no`
  - `trade_request_no` → `t_trade_relate_order.trade_request_no`

## 校验点(QA 关注)
- `orig_trx_voucher_no` 必须能在 `t_trade_transaction` 中找到对应原交易记录
- 退款的 `transaction_currency` / `pay_currency` 应与原交易币种一致
- `transaction_amount` 不应超过原交易的 `transaction_amount`（部分退/全退场景）
- `return_profit_amount` 与原交易的 `profit_amount` 关系需校验（退款应回退利润）
- `transaction_status` 状态流转需符合退款业务规则
- `trade_request_no` 应能关联到 `t_trade_relate_order` 中对应的退款类型订单
