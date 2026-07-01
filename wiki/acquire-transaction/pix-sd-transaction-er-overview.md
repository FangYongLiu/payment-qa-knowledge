---
title: pix SD-Transaction 数据库ER概览
domain: acquire-transaction
kind: wiki_page
slug: pix-sd-transaction-er-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:49c5a737-48df-4836-9baa-414f1de4f810
tags: []
related_services:
  - svc_pix
related_tables:
  - tbl_pix_refund_transaction
  - tbl_pix_t_refund_transaction
  - tbl_pix_t_trade_relate_order
  - tbl_pix_t_trade_transaction
  - tbl_pix_t_trade_transaction_extend
  - tbl_pix_trade_relate_order
  - tbl_pix_trade_transaction
  - tbl_pix_trade_transaction_extend
---

# pix SD-Transaction 数据库ER概览

本页概述 `pix` schema 下交易与退款相关表的实体关系，涵盖交易主表、退款表、关联订单表与扩展表四张表的结构与连接关系。

## 涉及的表

- [[tbl_pix_t_trade_transaction]] — 交易主表 `pix.t_trade_transaction`
- [[tbl_pix_t_refund_transaction]] — 退款交易表 `pix.t_refund_transaction`
- [[tbl_pix_t_trade_relate_order]] — 交易关联订单表 `pix.t_trade_relate_order`
- [[tbl_pix_t_trade_transaction_extend]] — 交易扩展表 `pix.t_trade_transaction_extend`

## 实体关系

- `t_trade_transaction` 与 `t_refund_transaction` 通过原始交易凭证号关联：退款表的 `orig_trx_voucher_no` 指向交易主表的 `trx_voucher_no`。
- `t_trade_relate_order` 通过 `trx_voucher_no` 关联到 `t_trade_transaction` / `t_refund_transaction`，承载 `trade_request_no` 与交易凭证号之间的映射。
- `t_trade_transaction_extend` 作为 `t_trade_transaction` 的扩展表，挂接附加字段。

## 关键主键与外键

- `t_trade_transaction.trx_voucher_no`（PK，bigint）— 交易主键
- `t_refund_transaction.trx_voucher_no`（PK，bigint）— 退款主键
- `t_refund_transaction.orig_trx_voucher_no`（bigint）— 关联原交易
- `t_trade_relate_order.trade_request_no`（PK，bigint）— 交易请求主键
- `t_trade_relate_order.trx_voucher_no`（bigint）— 关联交易/退款凭证号

## 公共字段约定

交易与退款表共用一组金额/币种/状态字段，便于统一处理：

- 金额币种：`transaction_amount` / `transaction_currency`、`pay_amount` / `pay_currency`
- 状态与结果：`transaction_status`、`unity_result_code`、`channel_result_code`
- 利润相关：交易表 `profit_amount`、退款表 `return_profit_amount`

## 主要业务字段说明

- 交易主表特有：`channel_code`、`order_type`、`member_id`、`rate_version`、`margin_version`、`paid_time`
- 退款表特有：`refund_order_type`、`orig_trx_voucher_no`、`trade_request_no`
- 关联订单表特有：`transaction_type`、`trade_type`、`trade_order_status`

## 详细字段

各表完整字段定义见对应明细页：

- 交易主表字段 → [[tbl_pix_t_trade_transaction]]
- 退款交易表字段 → [[tbl_pix_t_refund_transaction]]
- 交易关联订单表字段 → [[tbl_pix_t_trade_relate_order]]
- 交易扩展表字段 → [[tbl_pix_t_trade_transaction_extend]]
