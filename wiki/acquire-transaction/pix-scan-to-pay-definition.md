---
title: PIX Scan to Pay 渠道定义与差异
domain: acquire-transaction
kind: wiki_page
slug: pix-scan-to-pay-definition
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:dae1b5ba-4844-4042-988d-9c537a25d281
tags: []
---

# PIX Scan to Pay 渠道定义与差异

本页定义 PIX Scan to Pay 场景下 AliPay / UnionPay / WeChat / Aani 四个渠道在商户信息展示、折扣、汇率计算与结算、订单字段上的关键差异。

## 金额定义

- **Transaction Amount(TrxAmount)**：币种为商户应收币种(merchant receivable currency)，如 CNY。
- **Payment Amount**：币种为 PayBy 币种，默认 AED。

## 商户信息展示

| 项 | AliPay | UnionPay | WeChat | Aani |
|---|---|---|---|---|
| Merchant Name | ✅ | ✅ | ✅ | — |
| Merchant Address | ✅ | Only City | ✅ | — |
| Merchant Logo | ❌ | ❌ | ❌ | — |
| TipsFee | ❌ | ✅ | ❌ | — |

## 折扣支持(Merchant Discount)

- **AliPay**：✅ Decode code
- **UnionPay**：Discount Payment Amount ✅(Create Trade Order)
- **WeChat**：Discount Transaction Amount
- **Aani**：❌

## 汇率(ExchangeRate)计算与结算方

- **AliPay**：Allow Margin；Calc → By PayBy；Settle → By Ali
  - 在 A+ 提供的汇率基础上加收 extra margin fee
- **UnionPay**：Allow Margin；Calc → By PayBy；Settle → By UPI
  - 在 Exchange Service 提供的汇率基础上加收 extra margin fee
  - 当 UnionPay place order amount 超过 payment amount(After exchange) 时拒绝该笔交易
- **WeChat**：Allow Margin；Calc → By PayBy；Settle → By PayBy
  - 汇率由 PayBy 提供
- **Aani**：No Need(无需汇率换算)

## 订单字段(Order Code)

| 字段 | AliPay | UnionPay | WeChat | Aani |
|---|---|---|---|---|
| Description | ✅ | ✅ | ✅ | — |
| TrxAmount | ✅ | ✅ | ✅ | — |
| PaymentAmount | By PayBy | By UPI(Create Trade Order) | By PayBy | — |
