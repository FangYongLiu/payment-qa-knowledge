---
title: Cashdesk 提现出款时序流程
domain: withdraw-cash
kind: wiki_page
slug: cashdesk-fundout-sequence
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:ce83da2f-919c-4d5c-8b5c-cb3d2ee5cac3
tags: []
---

# Cashdesk 提现出款时序流程

本页描述 Cashdesk "Add funds" 出款的端到端调用时序，覆盖前端鉴权/校验、CardToken 创建、FundOut 支付链路，以及 CMF 批次申请与 H2H 对接 BANK 的定时 job。相关业务流程见 [[flow_payby_cash_out]]。

## 参与方

- Timer（定时触发器）
- Customer
- app-sdk
- cgs
- cashdesk-api
- fundout
- pfs-payment
- payment
- grc-check-identity-provider
- cmf
- cmf-task
- h2h
- BANK

## 主流程：用户发起出款

1. Customer → app-sdk：发起 Add funds。
2. app-sdk → cgs：`/cashdesk/fundoutAuth`
   - cgs → cashdesk-api
   - cashdesk-api → grc-check-identity-provider：`PaymentSessionQueryStub#paymentSessionQuery`
3. app-sdk → cgs：`/cashdesk/verify`
   - cgs → cashdesk-api，依次触发：
     - cashdesk-api → cmf：`CardTokenFacade#create`（创建 CardToken）
     - cashdesk-api → fundout：`FundoutSimpleFacade#pay`
       - fundout → pfs-payment：`FundOutPaymentFacade#pay`
       - pfs-payment → payment：`PaymentFacade#pay`
       - payment → cmf：`FundRequestFacade#apply`
4. app-sdk ⇠ Customer：返回 `apply success`。

## 异步批处理：CMF 与 BANK 对接

由 Timer 周期性驱动 cmf-task，通过 h2h 与 BANK 交互：

- **batch request job**：Timer → cmf-task → h2h → BANK，将累积的出款请求批量提交银行。
- **batch query job**：Timer → cmf-task，定期查询批次/交易状态。

## 关键点

- `verify` 阶段在同一调用链内完成 CardToken 创建与 FundOut 支付申请，最终在 cmf 落地为 FundRequest。
- 用户侧仅同步收到 `apply success`，真正的银行出款由 cmf-task 的 request/query job 异步推进。
