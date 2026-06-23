---
id: flow_add_funds_deposit
object_type: Flow
domain: payby-open-api
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:5d857d21-abfb-434d-a195-7f7a84e5418b
tags:
- add-funds
- deposit
- 3ds
- confirm-pay
subdomain: null
module: null
sensitivity: normal
name: Add Funds 充值端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Add Funds 充值端到端时序流程，覆盖客户端从 app-sdk 发起 confirm-pay、verify，经 cgs/cashierii 调度核心交易、卡 token 创建、支付链路扣款，直至跳转 3DS 银行验证的关键节点。参与方：Customer、app-sdk、cgs、cashierii、grc-component-connect-provider、deposit、tradeii、pfs-payment、payment、cmf、qpay-cko、fcw、BANK。

## 步骤(跨系统)
1. Customer → app-sdk：submit deposit（提交充值）
   - 1.1 app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
     - 1.1.1 cgs → cashierii
       - 1.1.1.1 cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`
   - 1.2 app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
     - 1.2.1 cgs → cashierii
       - 1.2.1.1 cashierii → cmf：`CardTokenFacade#create`
       - 1.2.1.2 cashierii → tradeii：`CashierTradePayFacade#confirmPay`
         - 1.2.1.2.1 tradeii → pfs-payment：`QuickPayPaymentFacade#pay`
           - 1.2.1.2.1.1 pfs-payment → payment：`PaymentFacade#pay`
             - 1.2.1.2.1.1.1 payment → cmf：`FundRequestFacade#apply`
               - 1.2.1.2.1.1.1.1 cmf → qpay-cko：`ChannelFundFacade#apply`
                 - 1.2.1.2.1.1.1.1.1 qpay-cko → fcw
   - 1.3 app-sdk ⇠ Customer（返回）：3ds bank form
2. Customer → BANK：request and complete 3ds verify
3. BANK（返回）

## 涉及服务/表
- 服务：app-sdk、cgs、cashierii、grc-component-connect-provider、deposit、tradeii、pfs-payment、payment、cmf、qpay-cko、fcw
- 外部：BANK
- 接口：`/cashierii/pay/v1/auth/confirm-pay`、`/cashierii/pay/v1/auth/verify`、`PaymentSessionQueryStub#paymentSessionQuery`、`CardTokenFacade#create`、`CashierTradePayFacade#confirmPay`、`QuickPayPaymentFacade#pay`、`PaymentFacade#pay`、`FundRequestFacade#apply`、`ChannelFundFacade#apply`

## 校验点
- confirm-pay 阶段：通过 `PaymentSessionQueryStub#paymentSessionQuery` 校验支付会话
- verify 阶段：先 `CardTokenFacade#create` 创建卡 token，再 `CashierTradePayFacade#confirmPay` 进入交易扣款链路
- 扣款链路：tradeii → pfs-payment → payment → cmf → qpay-cko → fcw 顺序贯通
- 3DS：app-sdk 返回 3ds bank form，Customer 直接到 BANK 完成 3ds verify
