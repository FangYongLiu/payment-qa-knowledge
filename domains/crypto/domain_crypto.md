---
id: domain_crypto
object_type: Domain
name: crypto
aliases: [数字货币, 加密货币, CC, digital-asset]
domain: crypto
product: payment
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [crypto, 数字货币, CC, BTC, ETH, TRON]
related_services: [svc_ccdpm_accounting, svc_ccdpm_manager, svc_cc_channel_btc, svc_cc_channel_eth, svc_ccdpm_task, svc_cc_channel_tron, svc_holding, svc_cc_cashier, svc_cc_trade, svc_asset_info, svc_cc_acquire, svc_quotation, svc_crypto_currency_exchange, svc_cc_sales, svc_cc_deposit, svc_cc_transfer, svc_cc_withdraw]
---

# crypto(数字货币 / 加密货币)

> 业务域总览。数字货币(CC)业务线:交易/钱包/兑换/链上通道/记账。域 lead 待指定。

## 概述
Crypto 数字货币业务域:加密货币的买卖/充提/转账/交易/收银/兑换、行情报价、持仓,
以及链上通道(BTC/ETH/TRON)与数字货币记账(ccdpm)。此前散落在 online-business 与
payment-core,现统一收拢。

## 覆盖范围
- 交易/钱包(online-business 迁入):cc-sales/withdraw/deposit/transfer/trade/cashier/acquire、
  asset-info、holding、quotation、crypto-currency-exchange
- 链上通道(payment-core 迁入):cc-channel-eth/btc/tron
- 数字货币记账(payment-core 迁入):ccdpm-accounting/manager/task

## QA 关注点
- 待补。
