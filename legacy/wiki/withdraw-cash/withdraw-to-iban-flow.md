---
title: 提现到UAE银行(IBAN)流程
domain: withdraw-cash
kind: wiki_page
slug: withdraw-to-iban-flow
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PCW/1972174889
tags: []
---

# 提现到UAE银行(IBAN)流程

本页描述用户将钱包余额提现到 UAE 本地银行账户（IBAN）的端到端调用链，分为 Place Order（下单）与 Pay（支付）两个阶段。Aani 渠道见 [[withdraw-to-aani-flow]]，整体业务视角见 [[flow_payby_withdraw_to_bank]]。

## 参与角色与服务

- Customer：发起提现的终端用户
- app-sdk：客户端 SDK
- cgs：网关层
- personal：个人账户域
- fundout：出金域服务
- cashdesk-api：收银台 API
- pfs-payment：支付前置
- payment：支付核心
- cmf / cmf-task：资金移动框架及其任务调度
- grc-check-identity-provider：身份校验
- h2h：对接银行的通道
- BANK：UAE 本地银行
- Timer：定时任务触发器

## Step 1: Place Order（下单阶段）

用于创建提现订单并初始化收银台页面。

调用链：

1. Customer → app-sdk 发起提现
2. app-sdk → cgs：`/personal/transfer/bank/submit`
3. cgs → personal
4. personal → fundout：`CashierFundoutFacade#createCashierFundout`
5. fundout → cashdesk-api：`TokenServiceFacade#getFundoutToken`
6. cashdesk-api → fundout → personal → cgs，逐层返回
7. cgs → app-sdk：返回 `cashierUrl`
8. app-sdk → cgs：`/cashdesk/unityInitPayPage`
9. cgs → cashdesk-api → cgs → app-sdk → Customer，渲染收银台

## Step 2: Pay（支付阶段）

支付阶段细分为 Auth、Verify、Batch Request Job、Batch Query Job 四段。

### Pay - Auth（鉴权）

1. Customer → app-sdk → cgs：`/cashdesk/fundoutAuth`
2. cgs → cashdesk-api
3. cashdesk-api → grc-check-identity-provider：`PaymentSessionQueryStub#paymentSessionQuery`

### Pay - Verify（身份校验与发起支付）

1. Customer → app-sdk
2. app-sdk 本地执行 `Verify identity`
3. app-sdk → cgs：`/cashdesk/verify`
4. cgs → cashdesk-api
5. cashdesk-api → cmf：`CardTokenFacade#create`
6. cashdesk-api → fundout：`FundoutSimpleFacade#pay`
7. fundout → pfs-payment：`FundOutPaymentFacade#pay`
8. pfs-payment → payment：`PaymentFacade#pay`
9. payment → cmf：`FundRequestFacade#apply`

### Batch Request Job（批量请求）

由 Timer 触发：

- Timer → cmf-task → h2h → BANK

向银行批量发起出金请求。

### Batch Query Job（批量查询）

由 Timer 触发，并将结果异步回流：

- Timer → cmf-task → h2h → BANK
- cmf-task ⇢ payment ⇢ pfs-payment ⇢ fundout（异步状态回传）

## 关键接口一览

| 阶段 | 接口 / 方法 |
|---|---|
| Place Order | `/personal/transfer/bank/submit` |
| Place Order | `CashierFundoutFacade#createCashierFundout` |
| Place Order | `TokenServiceFacade#getFundoutToken` |
| Place Order | `/cashdesk/unityInitPayPage` |
| Pay - Auth | `/cashdesk/fundoutAuth` |
| Pay - Auth | `PaymentSessionQueryStub#paymentSessionQuery` |
| Pay - Verify | `/cashdesk/verify` |
| Pay - Verify | `CardTokenFacade#create` |
| Pay - Verify | `FundoutSimpleFacade#pay` |
| Pay - Verify | `FundOutPaymentFacade#pay` |
| Pay - Verify | `PaymentFacade#pay` |
| Pay - Verify | `FundRequestFacade#apply` |
