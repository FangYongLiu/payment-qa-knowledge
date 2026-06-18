---
id: tbl_trade_db
object_type: Table
domain: payment-databases
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 交易
- 收单
- 退款
- 出款
- 转账
- 充值
- 提现
subdomain: trade
module: null
sensitivity: normal
name: 交易类核心表
aliases: []
related_services: []
related_tables:
- tbl_member_db
- tbl_dpm_db
- tbl_merchant_db
- tbl_statement_db
- tbl_pricing_db
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
覆盖交易域核心库表，包含收单、退款、出款、个人转账，以及中台交易（充值、交易、提现）相关订单与支付信息，用于支付交易全链路数据查询与核对。

## 关键列
### 交易类
- `acquireii.t_acquire_order` —— 收单交易表
- `acquireii.t_payment_info` —— 收单支付信息表
- `acquireii.t_refund_order` —— 收单退款订单表
- `mhtfundout.t_fundout_order` —— 出款服务订单表
- `mhtfundout.t_payment_info` —— 出款服务支付信息表
- `mhtfundout.t_fundout_account_beneficiary` —— 出款服务收款方信息表
- `transfer.t_transfer_order` —— 个人转账

### 中台交易类
- `deposit.t_deposit_order` —— 充值
- `tradeii.t_trade_order` —— 交易
- `tradeii.t_order_ext` —— 交易订单扩展表
- `tradeii.t_payment_order` —— 交易支付订单表
- `fundout.tt_fundout_order` —— 提现

## 主键/索引
原文未提供主键/索引信息。

## 校验点(QA 关注)
- 收单链路：`t_acquire_order` 与 `t_payment_info`、`t_refund_order` 的订单关联与状态一致性。
- 出款链路：区分 `mhtfundout.t_fundout_order`（出款服务）与 `fundout.tt_fundout_order`（中台提现）两类不同的出款表。
- 中台交易：`tradeii.t_trade_order`、`t_order_ext`、`t_payment_order` 三表的订单/扩展/支付订单关联。
- 充值与提现分别落库 `deposit.t_deposit_order` 与 `fundout.tt_fundout_order`。
- 个人转账落库 `transfer.t_transfer_order`，与收单/中台交易表区分使用。
