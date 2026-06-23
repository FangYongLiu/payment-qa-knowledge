---
title: ToC Add Funds 充值流程时序
domain: payby-open-api
kind: wiki_page
slug: toc-add-funds-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:8c8c7ab8-1a68-4094-8122-e39339597e3f
tags: []
---

# ToC Add Funds 充值流程时序

本页描述 ToC 场景下客户端发起充值（submit deposit）后，经 app-sdk → cgs → cashierii → 下游交易/支付/记账组件的两阶段调用时序，以及支付完成后的异步结果处理链路。

## 参与方

时序图涉及的 lifeline（自左至右）：

- Customer（actor）
- app-sdk
- cgs
- cashierii
- grc-component-connect-provider
- transfer
- tradeii
- pfs-payment
- payment
- dpm-accounting

## 主流程：submit deposit

客户端发起充值后，由 app-sdk 经 cgs 调用 cashierii 完成两阶段交互（confirm-pay + verify），最终落到 payment / dpm-accounting 完成扣款与记账。

1. Customer → app-sdk：submit deposit
2. 1.1 app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
   - 1.1.1 cgs → cashierii
     - 1.1.1.1 cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`
3. 1.2 app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
   - 1.2.1 cgs → cashierii
     - 1.2.1.1 cashierii → tradeii：`CashierTradePayFacade#confirmPay`
       - 1.2.1.1.1 tradeii → pfs-payment：`BalancePaymentFacade#pay`
         - 1.2.1.1.1.1 pfs-payment → payment：`PaymentFacade#pay`
           - 1.2.1.1.1.1.1 payment → dpm-accounting：`AccountingFacade#apply`
4. 1.3 app-sdk ⇢ Customer（虚线返回）：payment result

## 两阶段调用说明

- 第一阶段 `confirm-pay`：cashierii 通过 `PaymentSessionQueryStub#paymentSessionQuery` 向 grc-component-connect-provider 查询支付会话信息。
- 第二阶段 `verify`：cashierii 触发 `CashierTradePayFacade#confirmPay`，向下逐层调用：
  - tradeii 通过 `BalancePaymentFacade#pay` 调度余额支付；
  - pfs-payment 通过 `PaymentFacade#pay` 进入核心支付；
  - payment 通过 `AccountingFacade#apply` 调用 dpm-accounting 完成记账。
- 同步阶段结束后，app-sdk 将 payment result 返回给 Customer。

## 异步结果处理（process result）

支付完成后由 payment 触发的异步链路，用于结果回流与后续转账处理：

- 2 payment：process result（自调用）
  - 2.1 payment → pfs-payment
    - 2.1.1 pfs-payment → tradeii
      - 2.1.1.1 tradeii → transfer（图中以高亮/蓝色箭头标识）
