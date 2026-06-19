---
title: 银行卡充值端到端流程
domain: payby-core-systems
kind: wiki_page
slug: add-funds-via-bank-card-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:30b14d13-f138-4933-9a9e-82e4ba95aaa6
tags: []
---

# 银行卡充值端到端流程

通过银行卡向 PayBy 账户充值的端到端时序，分为「下单」与「卡支付」两个阶段，覆盖从 SDK 提交到银行 3DS 校验及支付结果回调的完整链路。相关业务背景见 [[add-funds-overview]]，时序图原图见 [[flow_add_funds_via_bank_card]]。

## 范围与说明

- 仅覆盖主流程系统调用。
- 已省略的查询类操作：会员、商户、费用计算、结算周期、商户支付方式鉴权查询、风控识别、渠道路由等。
- 不建议在新系统设计图中加入此类间接依赖系统。

## 参与角色与系统

- Customer：最终用户
- app-sdk：客户端 SDK
- cgs：网关
- personal：个人业务域
- deposit：充值领域
- tradeii：交易域
- cashierii：收银台
- grc-component-connect-provider：支付会话查询组件
- pfs-payment、payment：支付服务
- cmf：资金/卡管理
- qpay-cko：快捷支付渠道
- fcw：支付结果回调网关
- BANK：发卡行

## Step 1：Place Order（下单）

下单阶段由 SDK 提交充值请求，经 cgs 串联个人/充值/交易/收银台，最终返回 `tokenUrl` 用于跳转支付。

调用顺序：

1. Customer → sdk：submit deposit
2. sdk → cgs：`/personal/deposit/v1/auth/submit`
3. cgs → personal → deposit
4. deposit → tradeii：`CashierDepositFacade#createCashierDeposit`
5. tradeii → cashierii：`CashierTradeFacade#createCashierTrade`
6. cashierii：`OrderTokenFacade#getTradeOrderToken` 返回 `cashierToken`
7. 逐层回传至 sdk，得到 `tokenUrl`
8. sdk → cgs：`/cashierii/order/v1/auth/init-trade`
9. cgs → cashierii，结果回传 Customer

## Step 2：Card Pay（卡支付）

卡支付阶段包含确认支付、身份验证、银行扣款、3DS 校验和异步结果回调。

### 确认支付

1. Customer → sdk：submit deposit
2. sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
3. cgs → cashierii
4. cashierii → grc：`PaymentSessionQueryStub#paymentSessionQuery`

### 身份验证与发起扣款

1. sdk 本地 verify identity
2. sdk → cgs：`/cashierii/pay/v1/auth/verify`
3. cgs → cashierii
4. cashierii → cmf：`CardTokenFacade#create`
5. cashierii → tradeii：`CashierTradePayFacade#confirmPay`
6. tradeii → pfs：`QuickPayPaymentFacade#pay`
7. pfs → payment：`PaymentFacade#pay`
8. payment → cmf：`FundRequestFacade#apply`
9. cmf → qpay：`ChannelFundFacade#apply`
10. qpay → BANK
11. sdk 返回 Customer：3ds bank form

### 3DS 校验

- Customer → BANK：request and complete 3ds verify

### 支付结果回调

银行通过 fcw 异步回传结果，沿原链路反向通知至 deposit：

- BANK → fcw：pay result
- fcw → cmf → payment → pfs → tradeii → deposit
