---
id: reference_botim_transfer_overview
object_type: Reference
name: BOTIM Transfer 转账流程总览
aliases: [botim-transfer-overview]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
source_type: wiki
source_ref: confluence:PCW/1971847185
tags: [payment-core, wiki-overview]
related_services: [svc_cashierii, svc_cgs, svc_dpm_accounting, svc_grc_component_connect_provider, svc_payment, svc_personal, svc_pfs_payment, svc_tradeii]
related_tables: []
---


# BOTIM Transfer 转账流程总览

BOTIM Transfer 转账业务由两个时序步骤构成：**Step 1 下单（Place Order）** 与 **Step 2 余额支付（Balance Pay）**，覆盖从用户提交转账到完成扣款记账的完整服务交互链路。端到端细节见 [[flow_botim_transfer]]。

## 业务域

- domain：`fund-out-transfer`
- 业务场景：BOTIM 转账（出款）

## 参与方与服务组件

| 组件 | 角色 |
| --- | --- |
| Customer | 终端用户 |
| app-sdk | 客户端 SDK |
| cgs | 网关 |
| personal | 个人业务服务 |
| transfer | 转账服务 |
| tradeii | 交易服务 |
| cashierii | 收银台服务 |
| grc-component-connect-provider | GRC 连接组件 |
| pfs-payment | 支付前置服务 |
| payment | 支付核心 |
| dpm-accounting | 记账服务 |

## Step 1：Place Order（下单）

下单阶段完成转账受理与收银台 token 获取，最终把 `tokenUrl` 返回客户端并初始化交易。

主要时序：

1. Customer → app-sdk：`submit transfer`
2. app-sdk → cgs：`/personal/transfer/submit`
3. cgs → personal
4. personal → transfer：`TransferOrderFacade#recruitTransfer`
5. transfer → tradeii：`CashierTradeFacade#createCashierTrade`
6. tradeii → cashierii：`OrderTokenFacade#getTradeOrderToken`
7. cashierii 返回 `cashierToken`，沿 tradeii → transfer → personal → cgs 回传
8. cgs → app-sdk：返回 `tokenUrl`
9. app-sdk → cgs：`/cashierii/order/v1/auth/init-trade`
10. cgs → cashierii，返回结果回传至 app-sdk → Customer

## Step 2：Balance Pay（余额支付）

支付阶段在身份校验后驱动收银台、交易、支付与记账链路完成扣款。

主要时序：

1. Customer → app-sdk：`submit deposit`
2. app-sdk → cgs：`/cashierii/pay/v1/auth/confirm-pay`
3. cgs → cashierii
4. cashierii → grc-component-connect-provider：`PaymentSessionQueryStub#paymentSessionQuery`
5. Customer → app-sdk：`verify identity`（SDK 内部处理）
6. app-sdk → cgs：`/cashierii/pay/v1/auth/verify`
7. cgs → cashierii
8. cashierii → tradeii：`CashierTradePayFacade#confirmPay`
9. tradeii → pfs-payment：`BalancePaymentFacade#pay`
10. pfs-payment → payment：`PaymentFacade#pay`
11. payment → dpm-accounting：`AccountingFacade#apply`
12. app-sdk → Customer：返回 `payment result`
13. 异步回流：payment ⇒ pfs-payment ⇒ tradeii ⇒ transfer

## 关键接口与 Facade 速查

- 网关入口：
  - `/personal/transfer/submit`
  - `/cashierii/order/v1/auth/init-trade`
  - `/cashierii/pay/v1/auth/confirm-pay`
  - `/cashierii/pay/v1/auth/verify`
- 内部 Facade：
  - `TransferOrderFacade#recruitTransfer`
  - `CashierTradeFacade#createCashierTrade`
  - `OrderTokenFacade#getTradeOrderToken`
  - `PaymentSessionQueryStub#paymentSessionQuery`
  - `CashierTradePayFacade#confirmPay`
  - `BalancePaymentFacade#pay`
  - `PaymentFacade#pay`
  - `AccountingFacade#apply`

## 修订记录

| Date | Content | Revisor |
| --- | --- | --- |
| 23 Mar 2026 | BOTIM Transfer | Cong Zhou |
