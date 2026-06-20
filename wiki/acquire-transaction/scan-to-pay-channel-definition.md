---
title: Scan to Pay 各渠道字段与汇率定义对比
domain: acquire-transaction
kind: wiki_page
slug: scan-to-pay-channel-definition
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/537395306
tags: []
---

# Scan to Pay 各渠道字段与汇率定义对比

本页对比 AliPay、UnionPay、WeChat、Aani 四个渠道在 Scan to Pay 场景下，对商户信息、折扣、汇率与金额字段的支持差异。

## 金额定义

- **Transaction Amount**：以商户应收币种计价，例如 CNY。
- **Payment Amount**：以 PayBy 币种计价，默认 AED。

## 商户信息字段支持

| 字段 | AliPay | UnionPay | WeChat | Aani |
|---|---|---|---|---|
| Merchant Name | ✅ | ✅ | ✅ | — |
| Merchant Address | ✅ | Only City | ✅ | — |
| Merchant Logo | ❌ | ❌ | ❌ | — |
| TipsFee | ❌ | ✅ | ❌ | — |

## 折扣（Discount）支持

- **AliPay**：Merchant Discount（来源 Decode code）。
- **UnionPay**：Discount Payment Amount（来源 Create Trade Order）。
- **WeChat**：Discount Transaction Amount。
- **Aani**：❌ 不支持。

## 汇率（ExchangeRate）规则

- **AliPay**
  - Allow Margin
  - Calc → By PayBy
  - Settle → By Ali
  - 在 A+ 提供的汇率基础上加收额外 margin fee。
- **UnionPay**
  - Allow Margin
  - Calc → By PayBy
  - Settle → By UPI
  - 基于 Exchange Service 提供的汇率加收额外 margin fee；当 UnionPay 下单金额（换汇后）超过 payment amount 时拒绝该交易。
- **WeChat**
  - Allow Margin
  - Calc → By PayBy
  - Settle → By PayBy
  - 汇率由 PayBy 提供。
- **Aani**：No Need（无需换汇）。

## 订单与金额字段

| 字段 | AliPay | UnionPay | WeChat |
|---|---|---|---|
| Order Code Description | ✅ | ✅ | ✅ |
| TrxAmount | ✅ | ✅ | ✅ |
| PaymentAmount 来源 | By PayBy | By UPI（Create Trade Order） | By PayBy |
