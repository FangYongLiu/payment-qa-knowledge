---
title: Add Funds 充值支付时序流程
domain: payby-open-api
kind: wiki_page
slug: add-funds-deposit-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9b2e8f37-17da-4c43-ae67-c4ecfe942411
tags: []
---

# Add Funds 充值支付时序流程

本页描述 Add Funds 充值场景下，从 Customer 发起充值到 dpm-accounting 入账的端到端调用时序，以及各服务之间的交互关系。相关流程总览见 [[flow_add_funds_deposit]]。

## 参与方

时序图中涉及的参与方（从左至右）：

- Customer（用户）
- app-sdk
- cgs
- cashierii
- grc-component-connect-provider
- transfer
- tradeii
- pfs-payment
- payment
- dpm-accounting

## 主流程：提交充值并完成支付

主调用链由 Customer 发起 `submit deposit`，经过 app-sdk 调用 cgs 网关，最终下达至 dpm-accounting 完成账务处理。

### 1. Customer → app-sdk：submit deposit
用户在客户端提交充值请求。

### 1.1 确认支付（confirm-pay）
- **1.1** app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
- **1.1.1** cgs → cashierii
- **1.1.1.1** cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`

该步骤用于查询/校验支付会话。

### 1.2 验证并执行支付（verify）
- **1.2** app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
- **1.2.1** cgs → cashierii
- **1.2.1.1** cashierii → tradeii：`CashierTradePayFacade#confirmPay`
- **1.2.1.1.1** tradeii → pfs-payment：`BalancePaymentFacade#pay`
- **1.2.1.1.1.1** pfs-payment → payment：`PaymentFacade#pay`
- **1.2.1.1.1.1.1** payment → dpm-accounting：`AccountingFacade#apply`

该步骤完成下单确认 → 余额支付 → 支付处理 → 账务记账的逐层调用。

### 1.3 返回支付结果
app-sdk ⇢ Customer（虚线返回）：`payment result`，将支付结果回传给用户。

## 后置流程：处理结果回写

支付完成后，payment 侧触发结果处理并向上游回写：

- **2** payment 自循环：`process result`
- **2.1** payment → pfs-payment
- **2.1.1** pfs-payment → tradeii

用于将支付处理结果反向通知至 pfs-payment 与 tradeii，完成交易状态的最终更新。

## 关键接口一览

| 步骤 | 调用方 → 被调方 | 接口 |
|---|---|---|
| 1.1 | app-sdk → cgs | `/cashierii/pay/v1/auth/confirm-pay` |
| 1.1.1.1 | cashierii → grc-component-connect-provider | `PaymentSessionQueryStub#paymentSessionQuery` |
| 1.2 | app-sdk → cgs | `/cashierii/pay/v1/auth/verify` |
| 1.2.1.1 | cashierii → tradeii | `CashierTradePayFacade#confirmPay` |
| 1.2.1.1.1 | tradeii → pfs-payment | `BalancePaymentFacade#pay` |
| 1.2.1.1.1.1 | pfs-payment → payment | `PaymentFacade#pay` |
| 1.2.1.1.1.1.1 | payment → dpm-accounting | `AccountingFacade#apply` |
