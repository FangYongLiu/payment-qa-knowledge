---
id: tbl_pix_trade_relate_order
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:4538bf84-a043-4d3d-a9fd-d0fcbb9bc671
tags:
- pix
- trade
- relate-order
subdomain: pix
module: null
sensitivity: normal
name: PIX交易关联订单表 t_trade_relate_order
aliases:
- t_trade_relate_order
- pix.t_trade_relate_order
related_services:
- svc_pix
---

## 用途
PIX schema 下的交易请求与凭证号关联映射表，用于将 `trade_request_no`（交易请求号）映射到 `trx_voucher_no`（交易凭证号），并标识关联的交易类型与状态，串联 [[tbl_pix_trade_transaction]] 与 [[tbl_pix_refund_transaction]]。

## 关键列
- `trade_request_no` (bigint, PK) — 交易请求号
- `transaction_type` (varchar 10) — 交易类型
- `trx_voucher_no` (bigint) — 关联的交易凭证号
- `trade_type` (varchar 10) — 贸易类型
- `trade_order_status` (varchar 10) — 交易订单状态
- `unity_result_code` (varchar 50) — 统一结果码

## 主键/索引
- 主键：`trade_request_no`

## 校验点(QA 关注)
- `trade_request_no` 唯一，作为入口请求号能正确映射到 `trx_voucher_no`。
- `trx_voucher_no` 应能在 [[tbl_pix_trade_transaction]] 或 [[tbl_pix_refund_transaction]] 中找到对应记录（依据 `transaction_type` 区分支付/退款）。
- `transaction_type`、`trade_type`、`trade_order_status` 取值需符合枚举约定。
- `unity_result_code` 与关联交易表中的 `unity_result_code` 应保持一致。
