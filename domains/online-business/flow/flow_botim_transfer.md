---
id: flow_botim_transfer
object_type: Flow
name: BOTIM/ToC 转账与加款端到端流程
aliases: [BOTIM Transfer, ToC Add Funds, ToC Transfer]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PCW/1971847185
tags: [online-business, transfer, fundout, cashier, balance-pay]
related_services: [svc_cgs, svc_personal, svc_tradeii, svc_cashierii, svc_pfs_payment, svc_payment, svc_dpm_accounting, svc_fundout, svc_cashdesk_api, svc_grc_component_connect_provider]
related_tables: []
related_scenarios: []
---

# BOTIM/ToC 转账与加款端到端流程

## 概述
C 端(Botim App)发起的转账与加款链路。转账走 **下单(Place Order)+ 余额支付(Balance Pay)** 两阶段;加款(Add funds,银行转账方式)走收银台出款单链路。两者均经 app-sdk → [[svc_cgs]] 入口,由收银台 [[svc_cashierii]] 编排交易/支付/记账。

> 注:`app-sdk` 为客户端 SDK,非后端可部署服务,未建 Service 对象,仅在步骤中以文字出现。`transfer` 转账业务服务对象未单独建(待补)。

## 步骤(跨系统)
### A. 转账 Step 1 — Place Order(下单)
1. Customer → app-sdk:submit transfer
2. app-sdk → [[svc_cgs]]:`/personal/transfer/submit`
3. cgs → [[svc_personal]]
4. personal → transfer(转账服务,待补):`TransferOrderFacade#recruitTransfer`
5. transfer → [[svc_tradeii]]:`CashierTradeFacade#createCashierTrade`
6. tradeii → [[svc_cashierii]]:`OrderTokenFacade#getTradeOrderToken`
7. cashierii 返回 `cashierToken`,沿 tradeii → transfer → personal → cgs 回传,cgs → app-sdk 返回 `tokenUrl`
8. app-sdk → cgs:`/cashierii/order/v1/auth/init-trade`;cgs → cashierii(此阶段直连,跳过 personal/transfer/tradeii),原路返回

### B. 转账 Step 2 — Balance Pay(余额支付)
1. Customer → app-sdk:submit deposit
2. app-sdk → cgs:`/cashierii/pay/v1/auth/confirm-pay` → cgs → cashierii
3. cashierii → [[svc_grc_component_connect_provider]]:`PaymentSessionQueryStub#paymentSessionQuery`(查支付会话)
4. Customer 完成身份校验;app-sdk → cgs:`/cashierii/pay/v1/auth/verify` → cgs → cashierii
5. cashierii → tradeii:`CashierTradePayFacade#confirmPay`
6. tradeii → [[svc_pfs_payment]]:`BalancePaymentFacade#pay`
7. pfs-payment → [[svc_payment]]:`PaymentFacade#pay`
8. payment → [[svc_dpm_accounting]]:`AccountingFacade#apply`(记账)
9. 同步返回 payment result 给 Customer;随后 payment 异步回流 pfs-payment → tradeii → transfer

### C. 加款 Add Funds(银行转账方式)
1. Customer → app-sdk:发起加款
2. app-sdk → cgs:`/personal/transfer/bank/submit` → cgs → personal
3. personal → [[svc_fundout]]:`CashierFundoutFacade#createCashierFundout`(创建收银台出款单)
4. fundout → [[svc_cashdesk_api]]:`TokenServiceFacade#getFundoutToken`(获取出款 token)
5. 逐层回传 `cashierUrl` 至 app-sdk
6. app-sdk → cashdesk-api:`/cashdesk/unityInitPayPage`(初始化收银台页)→ 呈现给 Customer

### D. Botim 4.0.1 gRPC 入口处理(参考)
gRPC 订单请求 happy-path 内部时序:`BotimGrpcServiceImpl`(校验入参 + 反序列化 ApplicationMessage)→ `ReceiveOrderService.processRequest`(检查 API 配置 → `AppService.doService` 执行业务 → 加密/转换响应)→ `WriteResponseAssist`(写回 gRPC 响应)。

## 关联关系
- **经过的服务**:[[svc_cgs]] → [[svc_personal]] → [[svc_tradeii]] → [[svc_cashierii]] → [[svc_pfs_payment]] → [[svc_payment]] → [[svc_dpm_accounting]](转账);加款另经 [[svc_fundout]] → [[svc_cashdesk_api]];支付会话查询经 [[svc_grc_component_connect_provider]](= `related_services`)
- **关键表**:待补(转账/收银台落库表未在原文给出对象级映射)
- **关键场景**:待补(本流程暂无独立 Scenario 对象;商户侧出款见 [[scn_online_business_merchant_payout]])

## 关键接口与 Facade 速查
- 网关入口:`/personal/transfer/submit`、`/personal/transfer/bank/submit`、`/cashierii/order/v1/auth/init-trade`、`/cashierii/pay/v1/auth/confirm-pay`、`/cashierii/pay/v1/auth/verify`、`/cashdesk/unityInitPayPage`
- 内部 Facade:`TransferOrderFacade#recruitTransfer`、`CashierTradeFacade#createCashierTrade`、`OrderTokenFacade#getTradeOrderToken`、`CashierFundoutFacade#createCashierFundout`、`TokenServiceFacade#getFundoutToken`、`PaymentSessionQueryStub#paymentSessionQuery`、`CashierTradePayFacade#confirmPay`、`BalancePaymentFacade#pay`、`PaymentFacade#pay`、`AccountingFacade#apply`

## 校验点
- Step 1 完成时 cashierii 应返回有效 cashierToken,经 tradeii/transfer/personal/cgs 透传为 tokenUrl;`init-trade` 须在拿到 tokenUrl 后由 app-sdk 发起。
- Step 2 中 `confirm-pay` 后须先经 grc 组件做 paymentSessionQuery;身份校验(`verify`)通过后才触发 `confirmPay`。
- 余额支付链路 tradeii → pfs-payment → payment → dpm-accounting 顺序调用,记账由 `AccountingFacade#apply` 完成;支付结果先同步返回,再异步回流。
- 加款链路 `/personal/transfer/bank/submit` 须串通至 fundout `createCashierFundout` 并成功 `getFundoutToken`,cgs 正确回传 cashierUrl。
