---
id: flow_payby_withdraw_to_bank
object_type: Flow
domain: withdraw-cash
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:4efb14db-9f70-47c4-98d9-b2969c863ce6
tags:
- withdraw
- IBAN
- cashdesk
- fundout
subdomain: withdraw-to-iban
module: null
sensitivity: normal
name: 提现到银行卡端到端流程
aliases: []
related_services:
- app-sdk
- cgs
- personal
- fundout
- cashdesk-api
- pfs-payment
- payment
- grc-check-identity-provider
- cmf
- cmf-task
- h2h
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
提现到 UAE 银行卡（IBAN）端到端流程，覆盖 Place Order → Pay(Auth + Verify) → Batch Request Job / Batch Query Job 的跨系统服务交互。资金从用户余额账户转入银行卡，离开 PayBy 体系，由 cashdesk 收银台、fundout 提现域、pfs-payment、payment、cmf/cmf-task、h2h 与银行联动完成。

## 步骤(跨系统)

### Step 1: Place Order
1. Customer → app-sdk：发起提现下单。
2. app-sdk → cgs：`/personal/transfer/bank/submit`。
3. cgs → personal。
4. personal → fundout：`CashierFundoutFacade#createCashierFundout`。
5. fundout → cashdesk-api：`TokenServiceFacade#getFundoutToken`。
6. cashdesk-api → fundout → personal → cgs → app-sdk：返回 `cashierUrl`。
7. app-sdk → cgs：`/cashdesk/unityInitPayPage`。
8. cgs → cashdesk-api → cgs → app-sdk → Customer：初始化收银台页面。

### Step 2: Pay - Auth
1. Customer → app-sdk → cgs：`/cashdesk/fundoutAuth`。
2. cgs → cashdesk-api。
3. cashdesk-api → grc-check-identity-provider：`PaymentSessionQueryStub#paymentSessionQuery`，由风控返回需校验项。

### Step 2: Pay - Verify
1. Customer → app-sdk：sdk 内 `Verify identity`（核身）。
2. app-sdk → cgs：`/cashdesk/verify`。
3. cgs → cashdesk-api。
4. cashdesk-api → cmf：`CardTokenFacade#create`。
5. cashdesk-api → fundout：`FundoutSimpleFacade#pay`。
6. fundout → pfs-payment：`FundOutPaymentFacade#pay`。
7. pfs-payment → payment：`PaymentFacade#pay`。
8. payment → cmf：`FundRequestFacade#apply`。

### Batch Request Job
1. Timer → cmf-task。
2. cmf-task → h2h → BANK：批量向银行发起提现请求。

### Batch Query Job
1. Timer → cmf-task。
2. cmf-task → h2h → BANK：批量查询银行处理结果。
3. cmf-task →> payment →> pfs-payment →> fundout：异步回传结果，逐层更新订单/账单状态。

## 涉及服务/表
- 服务：app-sdk、cgs、personal、fundout、cashdesk-api、pfs-payment、payment、grc-check-identity-provider、cmf、cmf-task、h2h、BANK。
- 关键接口：
  - `/personal/transfer/bank/submit`
  - `/cashdesk/unityInitPayPage`
  - `/cashdesk/fundoutAuth`
  - `/cashdesk/verify`
  - `CashierFundoutFacade#createCashierFundout`
  - `TokenServiceFacade#getFundoutToken`
  - `PaymentSessionQueryStub#paymentSessionQuery`
  - `CardTokenFacade#create`
  - `FundoutSimpleFacade#pay`
  - `FundOutPaymentFacade#pay`
  - `PaymentFacade#pay`
  - `FundRequestFacade#apply`

## 校验点
- Place Order 阶段必须由 fundout 经 `TokenServiceFacade#getFundoutToken` 取得 token，cgs 才能拿到 `cashierUrl` 并初始化收银台。
- Pay-Auth 阶段由 cashdesk-api 调 grc-check-identity-provider `paymentSessionQuery` 决定核身项；Verify 必须在 sdk 完成 `Verify identity` 后才能继续。
- Verify 链路顺序：cashdesk-api → cmf(`CardTokenFacade#create`) → fundout(`FundoutSimpleFacade#pay`) → pfs-payment(`FundOutPaymentFacade#pay`) → payment(`PaymentFacade#pay`) → cmf(`FundRequestFacade#apply`)。
- 与银行实际交互发生在 Batch Request/Query Job：由 Timer 驱动 cmf-task → h2h → BANK，非同步实时。
- Batch Query Job 结果异步回传 payment → pfs-payment → fundout，作为最终成功/失败/退票状态来源。
