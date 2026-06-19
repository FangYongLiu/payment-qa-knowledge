---
title: BOTIM Transfer 转账流程
domain: fund-out-transfer
kind: wiki_page
slug: botim-transfer-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:63a56867-f8aa-4a98-8026-2854d0efb12f
tags: []
---

# BOTIM Transfer 转账流程

BOTIM 转账由 **Place Order（下单）** 与 **Balance Pay（余额支付）** 两个阶段组成，跨越 app-sdk、cgs、personal、transfer、tradeii、cashierii、pfs-payment、payment、dpm-accounting 等服务，业务域为 `fund-out-transfer`。

## 涉及的服务与角色

- Customer：发起转账与身份校验的终端用户
- app-sdk：客户端 SDK
- cgs：网关
- personal：个人业务服务
- transfer：转账服务
- tradeii：交易服务
- cashierii：收银台服务
- grc-component-connect-provider：GRC 组件
- pfs-payment：支付前置服务
- payment：支付核心
- dpm-accounting：记账服务

## Step 1：Place Order（下单）

用户提交转账请求，链路最终拿到 cashierToken / tokenUrl，并完成收银台 trade 初始化。

调用顺序：

1. Customer → app-sdk：submit transfer
2. app-sdk → cgs：`/personal/transfer/submit`
3. cgs → personal
4. personal → transfer：`TransferOrderFacade#recruitTransfer`
5. transfer → tradeii：`CashierTradeFacade#createCashierTrade`
6. tradeii → cashierii：`OrderTokenFacade#getTradeOrderToken`
7. cashierii 返回 cashierToken → tradeii → transfer → personal → cgs → app-sdk（tokenUrl）
8. app-sdk → cgs：`/cashierii/order/v1/auth/init-trade`
9. cgs → cashierii，再原路返回至 Customer

关键接口与方法：

- HTTP：`/personal/transfer/submit`、`/cashierii/order/v1/auth/init-trade`
- Facade：`TransferOrderFacade#recruitTransfer`、`CashierTradeFacade#createCashierTrade`、`OrderTokenFacade#getTradeOrderToken`

## Step 2：Balance Pay（余额支付）

用户在收银台确认支付并完成身份校验后，由 cashierii 驱动 tradeii → pfs-payment → payment → dpm-accounting 完成扣款与记账，结果异步回流。

调用顺序：

1. Customer → app-sdk：submit deposit
2. app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
3. cgs → cashierii
4. cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`
5. Customer → app-sdk：verify identity（SDK 内部处理）
6. app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
7. cgs → cashierii
8. cashierii → tradeii：`CashierTradePayFacade#confirmPay`
9. tradeii → pfs-payment：`BalancePaymentFacade#pay`
10. pfs-payment → payment：`PaymentFacade#pay`
11. payment → dpm-accounting：`AccountingFacade#apply`
12. app-sdk → Customer：返回 payment result
13. payment 内部处理后异步回执：payment → pfs-payment → tradeii → transfer

关键接口与方法：

- HTTP：`/cashierii/pay/v1/auth/confirm-pay`、`/cashierii/pay/v1/auth/verify`
- Facade：`PaymentSessionQueryStub#paymentSessionQuery`、`CashierTradePayFacade#confirmPay`、`BalancePaymentFacade#pay`、`PaymentFacade#pay`、`AccountingFacade#apply`

## 两阶段衔接要点

- Step 1 产出 cashierToken / tokenUrl 并完成 `init-trade`，为 Step 2 的 `confirm-pay` 提供会话上下文。
- Step 2 中支付结果先同步返回给客户端，再由 payment 异步回流至 pfs-payment → tradeii → transfer，完成转账业务侧的状态推进。

## 修订记录

- 2026-03-23：新增 BOTIM Transfer 流程（Cong Zhou）
