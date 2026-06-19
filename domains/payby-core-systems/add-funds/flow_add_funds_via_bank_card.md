---
id: flow_add_funds_via_bank_card
object_type: Flow
domain: payby-core-systems
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:30b14d13-f138-4933-9a9e-82e4ba95aaa6
tags:
- add-funds
- bank-card
- 3ds
- deposit
subdomain: add-funds
module: null
sensitivity: normal
name: 银行卡充值端到端流程
aliases:
- Add funds via Bank Card
related_services:
- app-sdk
- cgs
- personal
- deposit
- tradeii
- cashierii
- grc-component-connect-provider
- pfs-payment
- payment
- cmf
- qpay-cko
- fcw
related_tables: []
related_scenarios:
- add-funds-via-bank-card-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

银行卡充值端到端流程描述 Customer 通过 app-sdk 在 PayBy 客户端发起 Add Funds via Bank Card 的完整时序，覆盖两大阶段：

- **Step 1: Place Order**：客户端提交充值，由 cgs 路由至 personal → deposit → tradeii → cashierii，生成 cashierToken 并返回 tokenUrl，再由客户端调用 init-trade 完成下单初始化。
- **Step 2: Card Pay**：客户端提交支付确认与身份校验，cashierii 通过 cmf 创建卡 token，并由 tradeii → pfs-payment → payment → cmf → qpay-cko 串行下发至 BANK，客户端在银行端完成 3DS 校验后，BANK 通过 fcw 异步回调结果，逐级回传至 deposit。

> 注：本流程仅包含主链路系统调用，省略了 member、merchant、fee 计算、结算周期、商户支付方式认证查询、风控、渠道路由等查询/旁路操作。

## 步骤(跨系统)

### Step 1: Place Order(下单)

1. Customer → app-sdk: submit deposit
2. app-sdk → cgs: `/personal/deposit/v1/auth/submit`
3. cgs → personal
4. personal → deposit
5. deposit → tradeii: `CashierDepositFacade#createCashierDeposit`
6. tradeii → cashierii: `CashierTradeFacade#createCashierTrade`
7. cashierii: `OrderTokenFacade#getTradeOrderToken`
8. cashierii ⟶ tradeii: 返回 `cashierToken`
9. tradeii ⟶ deposit ⟶ personal ⟶ cgs ⟶ app-sdk: 返回 `tokenUrl`
10. app-sdk → cgs: `/cashierii/order/v1/auth/init-trade`
11. cgs → cashierii
12. cashierii ⟶ cgs ⟶ app-sdk ⟶ Customer

### Step 2: Card Pay(支付)

**Confirm Pay**

1. Customer → app-sdk: submit deposit
2. app-sdk → cgs: `/cashierii/pay/v1/auth/confirm-pay`
3. cgs → cashierii
4. cashierii → grc-component-connect-provider: `PaymentSessionQueryStub#paymentSessionQuery`

**Verify(身份校验与下单支付)**

5. Customer → app-sdk
6. app-sdk: verify identity(本地身份校验)
7. app-sdk → cgs: `/cashierii/pay/v1/auth/verify`
8. cgs → cashierii
9. cashierii → cmf: `CardTokenFacade#create`
10. cashierii → tradeii: `CashierTradePayFacade#confirmPay`
11. tradeii → pfs-payment: `QuickPayPaymentFacade#pay`
12. pfs-payment → payment: `PaymentFacade#pay`
13. payment → cmf: `FundRequestFacade#apply`
14. cmf → qpay-cko: `ChannelFundFacade#apply`
15. qpay-cko → BANK
16. app-sdk ⟶ Customer: 返回 3DS bank form

**3DS Verification**

17. Customer → BANK: request and complete 3DS verify

**Pay Result Callback(异步回调)**

18. BANK → fcw: pay result
19. fcw → cmf
20. cmf ⟹ payment(异步)
21. payment ⟹ pfs-payment(异步)
22. pfs-payment ⟹ tradeii(异步)
23. tradeii ⟹ deposit(异步)

## 涉及服务/表

**服务（按调用顺序）**

| 角色 | 服务 | 主要职责 |
|---|---|---|
| 客户端 | app-sdk | 发起 deposit、身份校验、承载 3DS bank form |
| 网关 | cgs | 接入 `/personal/deposit/v1/auth/submit`、`/cashierii/order/v1/auth/init-trade`、`/cashierii/pay/v1/auth/confirm-pay`、`/cashierii/pay/v1/auth/verify` |
| 个人侧 | personal | 个人充值入口 |
| 充值域 | deposit | `CashierDepositFacade#createCashierDeposit`，接收异步支付结果 |
| 交易域 | tradeii | `CashierTradeFacade#createCashierTrade`、`CashierTradePayFacade#confirmPay` |
| 收银台 | cashierii | `OrderTokenFacade#getTradeOrderToken`、init-trade、confirm-pay、verify |
| 风控/会话 | grc-component-connect-provider | `PaymentSessionQueryStub#paymentSessionQuery` |
| 快捷支付 | pfs-payment | `QuickPayPaymentFacade#pay` |
| 支付核心 | payment | `PaymentFacade#pay` |
| 资金/卡 | cmf | `CardTokenFacade#create`、`FundRequestFacade#apply` |
| 渠道 | qpay-cko | `ChannelFundFacade#apply` |
| 回调 | fcw | 接收 BANK 异步支付结果 |
| 外部 | BANK | 受理支付与 3DS 验证 |

**表**：原文未列出。

## 校验点

- **下单链路**：cashierToken / tokenUrl 必须在 Step 1 由 cashierii 生成并经 tradeii→deposit→personal→cgs 透传至 app-sdk，随后 `init-trade` 才能成功。
- **支付会话**：confirm-pay 阶段必须通过 grc-component-connect-provider 的 `paymentSessionQuery` 取得有效支付会话。
- **身份校验**：app-sdk 端 `verify identity` 通过后，才能调用 `/cashierii/pay/v1/auth/verify`。
- **卡 Token**：cashierii 在 verify 阶段调用 `CardTokenFacade#create`，是后续 confirmPay→pay 的前置条件。
- **同步链路完整性**：cashierii → tradeii → pfs-payment → payment → cmf → qpay-cko → BANK 串行成功，方能向 app-sdk 返回 3DS bank form。
- **3DS 完成**：必须由 Customer 在 BANK 侧完成 3DS verify。
- **异步回调闭环**：BANK → fcw → cmf → payment → pfs-payment → tradeii → deposit 必须逐级到达 deposit，充值才算最终完成。
