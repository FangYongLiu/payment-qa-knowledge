---
id: tbl_pix_t_refund_transaction
object_type: Table
domain: acquire-transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:49c5a737-48df-4836-9baa-414f1de4f810
tags:
- pix
- refund
- transaction
subdomain: pix
module: SD-Transaction
sensitivity: normal
name: pix退款交易表 t_refund_transaction
aliases:
- t_refund_transaction
- Refund Transaction
related_services: []
related_tables:
- tbl_pix_t_trade_transaction
- tbl_pix_t_trade_relate_order
- tbl_pix_t_trade_transaction_extend
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 `pix` schema，记录 pix 渠道的退款交易明细。通过 `orig_trx_voucher_no` 关联原交易凭证（`pix.t_trade_transaction.trx_voucher_no`），并通过 `trade_request_no` 与交易关联订单表 `pix.t_trade_relate_order` 衔接。

## 关键列
- `trx_voucher_no` bigint —— 退款交易凭证号（主键）
- `orig_trx_voucher_no` bigint —— 原交易凭证号（关联 `t_trade_transaction.trx_voucher_no`）
- `refund_order_type` varchar(10) —— 退款订单类型
- `transaction_amount` decimal(19,4) —— 交易金额
- `transaction_currency` char(3) —— 交易币种
- `pay_amount` decimal(19,4) —— 支付金额
- `pay_currency` char(3) —— 支付币种
- `return_profit_amount` decimal(19,4) —— 退还的利润金额
- `transaction_status` varchar(10) —— 退款交易状态
- `trade_request_no` bigint —— 交易请求号（关联 `t_trade_relate_order.trade_request_no`）
- （原文标注尚有更多字段被截断）

## 主键/索引
- 主键：`trx_voucher_no`
- 隐含外键关系：
  - `orig_trx_voucher_no` → `pix.t_trade_transaction.trx_voucher_no`
  - `trade_request_no` → `pix.t_trade_relate_order.trade_request_no`

## 校验点(QA 关注)
- `orig_trx_voucher_no` 必须能在 `t_trade_transaction` 中找到对应原交易，且原交易状态允许退款。
- 退款 `transaction_amount` / `pay_amount` 不应超过原交易对应金额，币种 `transaction_currency`、`pay_currency` 与原交易一致性校验。
- `return_profit_amount` 与原交易 `profit_amount` 对账：全额退款应全额冲回，部分退款按比例。
- `transaction_status` 状态机正确流转，与 `t_trade_relate_order.trade_order_status`、`unity_result_code` 保持一致。
- `trade_request_no` 与 `t_trade_relate_order` 中 `transaction_type` 为退款的记录可关联。
- 同一 `orig_trx_voucher_no` 多笔部分退款累加金额不得超出原交易金额。
