---
id: tbl_pix_db
object_type: Table
domain: acquire-transaction
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:f8c68c87-2f3d-4b9e-bdac-e7aa90a94ed4
tags:
- pix
- schema
- ER
subdomain: null
module: null
sensitivity: normal
name: pix库交易核心表
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
汇总 pix schema 下交易、退款、关联订单及扩展表的表结构，用于收单交易主链路的数据落库。来源：wiki 页面 "pix-SD-Transaction" 的 ER 图。

## 关键列

### pix.t_trade_transaction (Trade Transaction)
- `trx_voucher_no` bigint (PK)
- `channel_code` varchar(32)
- `order_type` varchar(32)
- `member_id` varchar(20)
- `transaction_amount` decimal(19,4)
- `transaction_currency` char(3)
- `pay_amount` decimal(19,4)
- `pay_currency` char(3)
- `rate_version` bigint
- `margin_version` bigint
- `profit_amount` decimal(19,4)
- `transaction_status` varchar(10)
- `unity_result_code` varchar(50)
- `channel_result_code` varchar(50)
- `paid_time` timestamp(3)

### pix.t_refund_transaction (Refund Transaction)
- `trx_voucher_no` bigint (PK)
- `orig_trx_voucher_no` bigint
- `refund_order_type` varchar(10)
- `transaction_amount` decimal(19,4)
- `transaction_currency` char(3)
- `pay_amount` decimal(19,4)
- `pay_currency` char(3)
- `return_profit_amount` decimal(19,4)
- `transaction_status` varchar(10)
- `trade_request_no` bigint
- (原文截断，存在更多字段)

### pix.t_trade_relate_order (Trade Relate Order)
- `trade_request_no` bigint (PK)
- `transaction_type` varchar(10)
- `trx_voucher_no` bigint
- `trade_type` varchar(10)
- `trade_order_status` varchar(10)
- `unity_result_code` varchar(50)

### pix.t_trade_transaction_extend (Trade Transaction Extend)
- (原文未给出具体字段)

## 主键/索引
- `pix.t_trade_transaction` PK：`trx_voucher_no`
- `pix.t_refund_transaction` PK：`trx_voucher_no`；关联原交易通过 `orig_trx_voucher_no`
- `pix.t_trade_relate_order` PK：`trade_request_no`；通过 `trx_voucher_no` 关联交易/退款
- `pix.t_trade_transaction_extend`：原文未明确

## 校验点(QA 关注)
- 交易与退款的金额/币种字段：`transaction_amount`/`transaction_currency` 与 `pay_amount`/`pay_currency` 是否一致落库。
- `transaction_status`、`unity_result_code`、`channel_result_code` 在不同状态下的取值与终态一致性。
- 退款表 `orig_trx_voucher_no` 必须能回链到 `t_trade_transaction.trx_voucher_no`。
- `t_trade_relate_order` 通过 `trade_request_no` 与 `trx_voucher_no` 串联交易/退款，关注 `transaction_type`、`trade_type`、`trade_order_status` 的组合合法性。
- `rate_version`、`margin_version` 在交易落库时是否正确写入；`profit_amount`/`return_profit_amount` 退款冲销逻辑。
- `paid_time` 仅在支付成功状态写入。
