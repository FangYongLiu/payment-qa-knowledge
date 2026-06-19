---
id: flow_add_funds_via_bank_card
object_type: Flow
domain: payby-core-systems
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:PCW/1412988949
tags:
- add-funds
- bank-card
- 3ds
- deposit
subdomain: add-funds
module: null
sensitivity: normal
name: 通过银行卡充值端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

本流程描述用户通过银行卡进行 Add Funds（充值）的端到端两阶段时序：
- **Step 1: Place Order** —— 由 app-sdk 发起 submit deposit，经 cgs → personal → deposit → tradeii → cashierii，生成 cashierToken 并初始化交易，返回 tokenUrl 给客户端。
- **Step 2: Card Pay** —— 由客户端发起 confirm-pay，经 cashierii 完成支付会话查询、身份验证（verify），创建卡 token 并调用支付链路（tradeii → pfs-payment → payment → cmf → qpay-cko → BANK），银行返回 3DS 表单由客户端完成验证，最后通过 fcw 异步回调结果。

注：此流程仅包含主流程系统调用，省略了 member、merchant、费用计算、结算周期、商户支付方式认证查询、风控识别、渠道路由等查询类操作。

## 步骤(跨系统)

### Step 1: Place Order

1. Customer → app-sdk: submit deposit
2. sdk → cgs: `POST /personal/deposit/v1/auth/submit`
3. cgs → personal
4. personal → deposit: `CashierDepositFacade#createCashierDeposit`
5. deposit → tradeii: `CashierTradeFacade#createCashierTrade`
6. tradeii → cashierii: `OrderTokenFacade#getTradeOrderToken`
7. cashierii → tradeii: 返回 `cashierToken`
8. tradeii → deposit → personal → cgs → sdk: 返回 `tokenUrl`
9. sdk → cgs: `POST /cashierii/order/v1/auth/init-trade`
10. cgs → cashierii → cgs → sdk → Customer

### Step 2: Card Pay

#### Confirm Pay
1. Customer → app-sdk: submit deposit
2. sdk → cgs: `POST /cashierii/pay/v1/auth/confirm-pay`
3. cgs → cashierii
4. cashierii → grc-component-connect-provider: `PaymentSessionQueryStub#paymentSessionQuery`

#### Verify
5. Customer → sdk → sdk: verify identity
6. sdk → cgs: `POST /cashierii/pay/v1/auth/verify`
7. cgs → cashierii
8. cashierii → cmf: `CardTokenFacade#create`
9. cashierii → tradeii: `CashierTradePayFacade#confirmPay`
10. tradeii → pfs-payment: `QuickPayPaymentFacade#pay`
11. pfs-payment → payment: `PaymentFacade#pay`
12. payment → cmf: `FundRequestFacade#apply`
13. cmf → qpay-cko: `ChannelFundFacade#apply`
14. qpay-cko → BANK
15. sdk → Customer: 返回 3ds bank form

#### 3DS Verification
16. Customer → BANK: 发起并完成 3DS 验证

#### Pay Result Callback
17. BANK → fcw: pay result
18. fcw → cmf
19. cmf →> payment
20. payment →> pfs-payment
21. pfs-payment →> tradeii
22. tradeii →> deposit

## 涉及服务/表

**服务（参与者）：**
- app-sdk
- cgs
- personal
- deposit
- tradeii
- cashierii
- grc-component-connect-provider
- cmf
- pfs-payment
- payment
- qpay-cko
- fcw
- BANK（外部银行）

**关键 Facade / 接口：**
- `CashierDepositFacade#createCashierDeposit`
- `CashierTradeFacade#createCashierTrade`
- `OrderTokenFacade#getTradeOrderToken`
- `PaymentSessionQueryStub#paymentSessionQuery`
- `CardTokenFacade#create`
- `CashierTradePayFacade#confirmPay`
- `QuickPayPaymentFacade#pay`
- `PaymentFacade#pay`
- `FundRequestFacade#apply`
- `ChannelFundFacade#apply`

**HTTP 入口：**
- `/personal/deposit/v1/auth/submit`
- `/cashierii/order/v1/auth/init-trade`
- `/cashierii/pay/v1/auth/confirm-pay`
- `/cashierii/pay/v1/auth/verify`

## 校验点

- **Place Order 阶段**：cashierii 通过 `OrderTokenFacade#getTradeOrderToken` 生成 `cashierToken`，并最终返回 `tokenUrl` 给客户端，作为后续支付入口。
- **Confirm Pay 阶段**：cashierii 调用 `PaymentSessionQueryStub#paymentSessionQuery` 查询支付会话。
- **身份验证（Verify）**：客户端在 sdk 内完成 verify identity 后，cashierii 通过 `CardTokenFacade#create` 创建卡 token。
- **3DS 验证**：qpay-cko 调用 BANK 后，sdk 向客户端返回 3ds bank form；客户端必须直接与 BANK 完成 3DS 验证。
- **支付结果回调链路**：BANK → fcw → cmf → payment → pfs-payment → tradeii → deposit，采用异步回传（`->>`），需保证各层结果正确传递并最终回写至 deposit。
