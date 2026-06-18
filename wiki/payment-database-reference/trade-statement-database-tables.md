---
title: 交易与账单库常用表
domain: payment-database-reference
kind: wiki_page
slug: trade-statement-database-tables
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:79d1eee0-a479-47fd-8b3d-ec12172156f3
tags: []
---

# 交易与账单库常用表

本页汇总收单、出款、转账、中台交易（充值/交易/提现）以及账单（statementii）相关的核心数据库与表。其他业务域见 [[common-database-tables-guide]]。

## 收单交易（acquireii）

- `acquireii.t_acquire_order` —— 收单交易表
- `acquireii.t_payment_info` —— 收单支付信息表
- `acquireii.t_refund_order` —— 收单退款订单表

## 出款服务（mhtfundout）

- `mhtfundout.t_fundout_order` —— 出款服务订单表
- `mhtfundout.t_payment_info` —— 出款服务支付信息表
- `mhtfundout.t_fundout_account_beneficiary` —— 出款服务收款方信息表

## 个人转账（transfer）

- `transfer.t_transfer_order` —— 个人转账订单表

## 中台交易（deposit / tradeii / fundout）

充值：
- `deposit.t_deposit_order` —— 充值订单

交易：
- `tradeii.t_trade_order` —— 交易主单
- `tradeii.t_order_ext` —— 交易订单扩展表
- `tradeii.t_payment_order` —— 交易支付订单表

提现：
- `fundout.tt_fundout_order` —— 提现订单

## 账单（statementii）

- `statementii.t_statement_period` —— 账期表
- `statementii.t_statement_registration` —— 对账单登记表
- `statementii.t_statement_template` —— 对账单模板
- `statementii.t_statement_task` —— 对账单任务
- `statementii.t_statement_file` —— 对账单文件
- `statementii.t_statement_pruchase_statistics` —— 收单对账单信息统计

## 关联参考

- 商户、门店、账期、定时出款等参见 [[merchant-device-database-tables]]
- 会员账户、外部账户余额明细参见 [[member-database-tables]]
- 费率配置与策略相关表参见 [[pricing-database-tables]]
