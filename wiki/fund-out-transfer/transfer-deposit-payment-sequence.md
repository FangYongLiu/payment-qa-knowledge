---
title: Transfer 充值支付时序流程
domain: fund-out-transfer
kind: wiki_page
slug: transfer-deposit-payment-sequence
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e54e34ad-c773-4464-b860-83effe2987f7
tags: []
---

# Transfer 充值支付时序流程

本页描述客户在 Transfer 业务域 (domain=fund-out-transfer) 中发起 **Add funds** 充值时，从 app-sdk 经 cashierii、tradeii、pfs-payment 到 dpm-accounting 的端到端调用时序。

## 参与方

- **Customer**：发起充值的客户
- **app-sdk**：客户端 SDK
- **cgs**：网关
- **cashierii**：收银台
- **grc-component-connect-provider**：支付会话查询组件
- **transfer**：转账业务域
- **tradeii**：交易服务
- **pfs-payment**：支付服务
- **payment**：支付核心
- **dpm-accounting**：记账服务

## 主流程：提交充值 (submit deposit)

客户在 app-sdk 上点击 submit deposit，触发以下两段交互。

### 1.1 确认支付（confirm-pay）

- `1.1` app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
- `1.1.1` cgs → cashierii
- `1.1.1.1` cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`

用于在确认支付前查询支付会话。

### 1.2 校验并执行支付（verify）

- `1.2` app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
- `1.2.1` cgs → cashierii
- `1.2.1.1` cashierii → tradeii：`CashierTradePayFacade#confirmPay`
- `1.2.1.1.1` tradeii → pfs-payment：`BalancePaymentFacade#pay`
- `1.2.1.1.1.1` pfs-payment → payment：`PaymentFacade#pay`
- `1.2.1.1.1.1.1` payment → dpm-accounting：`AccountingFacade#apply`

调用链按 cashierii → tradeii → pfs-payment → payment → dpm-accounting 逐层下沉，最终由 dpm-accounting 完成记账。

### 1.3 返回支付结果

- app-sdk ⇢ Customer：返回 `payment result`（虚线返回）

## 异步流程：处理结果 (process result)

支付完成后由 payment 触发结果处理回流。

- `2` payment 自调用：`process result`
- `2.1` payment → pfs-payment
- `2.1.1` pfs-payment → tradeii

结果沿 payment → pfs-payment → tradeii 反向回传，用于交易状态的后续处理。

## 关键接口一览

| 层级 | 接口 |
|---|---|
| app-sdk → cgs | `/cashierii/pay/v1/auth/confirm-pay` |
| app-sdk → cgs | `/cashierii/pay/v1/auth/verify` |
| cashierii → grc-component-connect-provider | `PaymentSessionQueryStub#paymentSessionQuery` |
| cashierii → tradeii | `CashierTradePayFacade#confirmPay` |
| tradeii → pfs-payment | `BalancePaymentFacade#pay` |
| pfs-payment → payment | `PaymentFacade#pay` |
| payment → dpm-accounting | `AccountingFacade#apply` |
