---
id: flow_payby_cash_out
object_type: Flow
domain: withdraw-cash
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:ce83da2f-919c-4d5c-8b5c-cb3d2ee5cac3
tags:
- cashdesk
- fundout
- payby
subdomain: null
module: null
sensitivity: normal
name: PayBy 现金提现交易流程
aliases: []
related_services:
- app-sdk
- cgs
- cashdesk-api
- fundout
- pfs-payment
- payment
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
用户有将 PayBy 余额直接提现为现金（而非进入银行卡）的需求时，通过线下商户使用 POS 机完成现金提现交易。用户出示付款码，POS 机扫码识别后进行用户核身，商户确认无误后将等额现金交给用户，交易完成。系统侧由 Cashdesk 出款链路承载，最终通过 cmf-task 批量任务对接 h2h 下发到 BANK。

## 步骤(跨系统)
线下交互步骤：
1. 用户出示付款码：用户在 PayBy 端生成并出示付款码。
2. POS 机扫码：商户使用 POS 机扫描用户的付款码。
3. 用户核身：对用户身份进行核验。
4. 商户确认并付现：商户确认交易信息后，将现金交付给用户。
5. 交易完成。

系统侧调用链（Cashdesk 出款时序，参考 [[cashdesk-fundout-sequence]]）：
1. Customer → app-sdk
   - 1.1 app-sdk → cgs：`/cashdesk/fundoutAuth`
     - 1.1.1 cgs → cashdesk-api
       - 1.1.1.1 cashdesk-api → grc-check-identity-provider：`PaymentSessionQueryStub#paymentSessionQuery`
   - 1.2 app-sdk → cgs：`/cashdesk/verify`
     - 1.2.1 cgs → cashdesk-api
       - 1.2.1.1 cashdesk-api → cmf：`CardTokenFacade#create`
       - 1.2.1.2 cashdesk-api → fundout：`FundoutSimpleFacade#pay`
         - 1.2.1.2.1 fundout → pfs-payment：`FundOutPaymentFacade#pay`
           - 1.2.1.2.1.1 pfs-payment → payment：`PaymentFacade#pay`
             - 1.2.1.2.1.1.1 payment → cmf：`FundRequestFacade#apply`
   - 1.3 app-sdk ⇠ Customer：`apply success`（异步返回）

批次任务（Timer 调度）：
2. Timer → cmf-task：batch request job
   - 2.1 cmf-task → h2h
     - 2.1.1 h2h → BANK
3. Timer → cmf-task：batch query job
   - 3.1 cmf-task →（查询结果回流）

## 涉及服务/表
- 服务：app-sdk、cgs、cashdesk-api、grc-check-identity-provider、fundout、pfs-payment、payment、cmf、cmf-task、h2h、BANK
- 关键接口：`/cashdesk/fundoutAuth`、`/cashdesk/verify`、`PaymentSessionQueryStub#paymentSessionQuery`、`CardTokenFacade#create`、`FundoutSimpleFacade#pay`、`FundOutPaymentFacade#pay`、`PaymentFacade#pay`、`FundRequestFacade#apply`
- 数据表：原文未提及。

## 校验点
- 用户付款码有效性（POS 机扫码识别）。
- 身份核验：`grc-check-identity-provider` 通过 `PaymentSessionQueryStub#paymentSessionQuery` 进行核身。
- 卡 Token 创建：`CardTokenFacade#create` 成功。
- 出款申请链路逐层成功：`FundoutSimpleFacade#pay` → `FundOutPaymentFacade#pay` → `PaymentFacade#pay` → `FundRequestFacade#apply`，最终 `apply success` 返回。
- 商户确认环节：核对后将现金交付给用户。
- 批次任务：cmf-task 的 batch request job 与 batch query job 正常运行，确保 h2h 与 BANK 的下发与回查闭环。
