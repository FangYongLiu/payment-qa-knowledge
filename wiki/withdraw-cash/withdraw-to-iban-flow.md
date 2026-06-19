---
title: 提现到UAE银行(IBAN)流程
domain: withdraw-cash
kind: wiki_page
slug: withdraw-to-iban-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:4efb14db-9f70-47c4-98d9-b2969c863ce6
tags: []
---

# 提现到UAE银行(IBAN)流程

通过 app-sdk 发起的 IBAN 提现，分为 Place Order 与 Pay 两个阶段；Pay 阶段又细分为 Auth、Verify 以及由定时任务驱动的批量请求/查询。该流程属于 `domain=withdraw-cash` 业务域。

## 阶段总览

- **Step 1: Place Order**：用户在 app-sdk 下单，cgs 链路下发到 personal/fundout，最终由 cashdesk-api 返回 `cashierUrl` 并初始化收银台。
- **Step 2: Pay**：分为 Auth、Verify 两个交互子阶段，以及 Batch Request Job、Batch Query Job 两个异步定时任务。

## Step 1: Place Order

下单链路（app-sdk → cgs → personal → fundout → cashdesk-api）：

1. Customer → app-sdk 发起提现。
2. app-sdk → cgs：`/personal/transfer/bank/submit`
3. cgs → personal → fundout：调用 `CashierFundoutFacade#createCashierFundout`
4. fundout → cashdesk-api：调用 `TokenServiceFacade#getFundoutToken`
5. 链路逐层返回，cgs 向 sdk 返回 `cashierUrl`。
6. app-sdk → cgs：`/cashdesk/unityInitPayPage`
7. cgs → cashdesk-api 完成收银台初始化，最终返回给 Customer。

## Step 2: Pay

### Pay - Auth

- Customer → app-sdk → cgs：`/cashdesk/fundoutAuth`
- cgs → cashdesk-api → grc-check-identity-provider：`PaymentSessionQueryStub#paymentSessionQuery`

### Pay - Verify

- Customer 在 app-sdk 完成身份校验（Verify identity）。
- app-sdk → cgs：`/cashdesk/verify`
- cgs → cashdesk-api，随后 cashdesk-api 触发：
  - cmf：`CardTokenFacade#create`
  - fundout：`FundoutSimpleFacade#pay`
- 支付链路下推：
  - fundout → pfs-payment：`FundOutPaymentFacade#pay`
  - pfs-payment → payment：`PaymentFacade#pay`
  - payment → cmf：`FundRequestFacade#apply`

### Batch Request Job

由 Timer 定时驱动：

- Timer → cmf-task → h2h → BANK，将提现请求批量下发到银行。

### Batch Query Job

由 Timer 定时驱动：

- Timer → cmf-task → h2h → BANK 查询批量结果。
- 结果异步回流：cmf-task ⇢ payment ⇢ pfs-payment ⇢ fundout。

## 相关流程

- 同业务域的另一种提现渠道：[[withdraw-to-aani-flow]]
- 端到端业务流程视角：[[flow_payby_withdraw_to_bank]]
