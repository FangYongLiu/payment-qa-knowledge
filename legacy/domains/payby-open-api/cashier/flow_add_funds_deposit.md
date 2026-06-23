---
id: flow_add_funds_deposit
object_type: Flow
domain: payby-open-api
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:9b2e8f37-17da-4c43-ae67-c4ecfe942411
tags:
- deposit
- add-funds
- cashier
- payment
subdomain: cashier
module: add-funds
sensitivity: normal
name: Add Funds 充值端到端流程
aliases:
- add-funds-deposit-flow
related_services:
- cashierii
- tradeii
- pfs-payment
- payment
- dpm-accounting
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Add Funds（充值）端到端时序流程：客户端 submit deposit 后，经 app-sdk → cgs → cashierii，先做 confirm-pay 与 verify 两步，依次下钻到 tradeii / pfs-payment / payment / dpm-accounting 完成入账，最后将 payment result 回传客户端，并由 payment 侧异步 process result 回流。

## 步骤(跨系统)
1. Customer → app-sdk：submit deposit
   - 1.1 app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
     - 1.1.1 cgs → cashierii
       - 1.1.1.1 cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`
   - 1.2 app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
     - 1.2.1 cgs → cashierii
       - 1.2.1.1 cashierii → tradeii：`CashierTradePayFacade#confirmPay`
         - 1.2.1.1.1 tradeii → pfs-payment：`BalancePaymentFacade#pay`
           - 1.2.1.1.1.1 pfs-payment → payment：`PaymentFacade#pay`
             - 1.2.1.1.1.1.1 payment → dpm-accounting：`AccountingFacade#apply`
   - 1.3 app-sdk ⇢ Customer（异步返回）：payment result
2. payment：process result（自调用）
   - 2.1 payment → pfs-payment
     - 2.1.1 pfs-payment → tradeii

## 涉及服务/表
- 服务：app-sdk、cgs、cashierii、grc-component-connect-provider、transfer、tradeii、pfs-payment、payment、dpm-accounting
- 关键 Facade/接口：
  - `PaymentSessionQueryStub#paymentSessionQuery`（grc-component-connect-provider）
  - `CashierTradePayFacade#confirmPay`（tradeii）
  - `BalancePaymentFacade#pay`（pfs-payment）
  - `PaymentFacade#pay`（payment）
  - `AccountingFacade#apply`（dpm-accounting）
- 网关路径：`/cashierii/pay/v1/auth/confirm-pay`、`/cashierii/pay/v1/auth/verify`

## 校验点
- confirm-pay 阶段需通过 `PaymentSessionQueryStub#paymentSessionQuery` 校验支付会话。
- verify 阶段链路：`CashierTradePayFacade#confirmPay` → `BalancePaymentFacade#pay` → `PaymentFacade#pay` → `AccountingFacade#apply`，任一环节失败影响最终 payment result。
- 1.3 payment result 回传客户端为同步返回；步骤 2 process result 为 payment 侧后处理，向 pfs-payment、tradeii 回流，需与 1.x 主链路一致。
