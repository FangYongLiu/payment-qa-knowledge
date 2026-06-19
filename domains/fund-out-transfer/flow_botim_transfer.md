---
id: flow_botim_transfer
object_type: Flow
domain: fund-out-transfer
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:PCW/1971847185
tags:
- BOTIM
- transfer
- balance-pay
subdomain: null
module: null
sensitivity: normal
name: BOTIM Transfer 端到端转账流程
aliases: []
related_services:
- app-sdk
- cgs
- personal
- transfer
- tradeii
- cashierii
- pfs-payment
- payment
- dpm-accounting
- grc-component-connect-provider
related_tables: []
related_scenarios:
- botim-transfer-overview
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

BOTIM Transfer 端到端转账流程分两步：Step 1 Place Order(下单获取 cashierToken 并初始化交易)，Step 2 Balance Pay(确认支付、身份校验后执行余额支付与记账)。流程跨 app-sdk、cgs、personal、transfer、tradeii、cashierii、pfs-payment、payment、dpm-accounting 等服务。

## 步骤(跨系统)

### Step 1: Place Order

1. Customer → app-sdk：submit transfer
2. app-sdk → cgs：`/personal/transfer/submit`
3. cgs → personal
4. personal → transfer：`TransferOrderFacade#recruitTransfer`
5. transfer → tradeii：`CashierTradeFacade#createCashierTrade`
6. tradeii → cashierii：`OrderTokenFacade#getTradeOrderToken`
7. cashierii ⇢ tradeii：返回 cashierToken
8. tradeii ⇢ transfer ⇢ personal ⇢ cgs ⇢ app-sdk：返回 tokenUrl
9. app-sdk → cgs：`/cashierii/order/v1/auth/init-trade`
10. cgs → cashierii；cashierii ⇢ cgs ⇢ app-sdk ⇢ Customer

### Step 2: Balance Pay

1. Customer → app-sdk：submit deposit
2. app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
3. cgs → cashierii
4. cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`
5. Customer → app-sdk：verify identity (sdk 自处理后)
6. app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
7. cgs → cashierii
8. cashierii → tradeii：`CashierTradePayFacade#confirmPay`
9. tradeii → pfs-payment：`BalancePaymentFacade#pay`
10. pfs-payment → payment：`PaymentFacade#pay`
11. payment → dpm-accounting：`AccountingFacade#apply`
12. app-sdk ⇢ Customer：返回 payment result
13. payment 内部处理后异步通知 pfs-payment ⇢ tradeii ⇢ transfer

## 涉及服务/表

- 服务：app-sdk、cgs、personal、transfer、tradeii、cashierii、pfs-payment、payment、dpm-accounting、grc-component-connect-provider
- 关键 Facade/接口：
  - `TransferOrderFacade#recruitTransfer`
  - `CashierTradeFacade#createCashierTrade`
  - `OrderTokenFacade#getTradeOrderToken`
  - `PaymentSessionQueryStub#paymentSessionQuery`
  - `CashierTradePayFacade#confirmPay`
  - `BalancePaymentFacade#pay`
  - `PaymentFacade#pay`
  - `AccountingFacade#apply`
- HTTP 路径：
  - `/personal/transfer/submit`
  - `/cashierii/order/v1/auth/init-trade`
  - `/cashierii/pay/v1/auth/confirm-pay`
  - `/cashierii/pay/v1/auth/verify`

## 校验点

- Step 1 完成时 cashierii 应返回有效 cashierToken，并经 tradeii/transfer/personal/cgs 透传至 app-sdk(tokenUrl)。
- `/cashierii/order/v1/auth/init-trade` 调用须在拿到 tokenUrl 后由 app-sdk 发起。
- Step 2 中 confirm-pay 之后，cashierii 须先经 grc-component-connect-provider 进行 paymentSessionQuery。
- 身份核验通过 `/cashierii/pay/v1/auth/verify` 完成后才会触发 `CashierTradePayFacade#confirmPay`。
- 余额支付链路：tradeii → pfs-payment → payment → dpm-accounting 顺序调用，记账由 `AccountingFacade#apply` 完成。
- 支付结果先返回 Customer(app-sdk)，随后 payment 异步回流至 pfs-payment → tradeii → transfer。
