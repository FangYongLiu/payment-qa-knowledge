---
id: tbl_pix_t_trade_transaction
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
- transaction
- ER
subdomain: pix
module: SD-Transaction
sensitivity: normal
name: pix交易主表 t_trade_transaction
aliases:
- t_trade_transaction
related_services: []
related_tables:
- tbl_pix_t_refund_transaction
- tbl_pix_t_trade_relate_order
- tbl_pix_t_trade_transaction_extend
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
pix schema 下的交易主表，记录 pix 渠道的交易凭证、金额、币种、状态以及渠道返回结果等核心信息。

## 关键列
- `trx_voucher_no` (bigint) — 交易凭证号，主键
- `channel_code` (varchar 32) — 渠道代码
- `order_type` (varchar 32) — 订单类型
- `member_id` (varchar 20) — 会员 ID
- `transaction_amount` (decimal 19,4) — 交易金额
- `transaction_currency` (char 3) — 交易币种
- `pay_amount` (decimal 19,4) — 支付金额
- `pay_currency` (char 3) — 支付币种
- `rate_version` (bigint) — 汇率版本
- `margin_version` (bigint) — 利润/差价版本
- `profit_amount` (decimal 19,4) — 利润金额
- `transaction_status` (varchar 10) — 交易状态
- `unity_result_code` (varchar 50) — 统一结果码
- `channel_result_code` (varchar 50) — 渠道结果码
- `paid_time` (timestamp 3) — 支付完成时间

## 主键/索引
- 主键：`trx_voucher_no`

## 校验点(QA 关注)
- `trx_voucher_no` 作为主键，需与 `t_trade_relate_order.trx_voucher_no`、`t_refund_transaction.orig_trx_voucher_no` 关联一致
- `transaction_amount` 与 `pay_amount` 在跨币种时通过 `rate_version` / `margin_version` 换算，需校验 `transaction_currency` 与 `pay_currency` 的合理组合
- `profit_amount` 与退款表 `return_profit_amount` 在退款场景下需对账一致
- `transaction_status` 状态流转与 `unity_result_code`、`channel_result_code` 的对应关系
- `paid_time` 仅在交易达到已支付状态时填充，需与 `transaction_status` 一致
