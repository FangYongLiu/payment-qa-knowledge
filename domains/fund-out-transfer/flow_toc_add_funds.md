---
id: flow_toc_add_funds
object_type: Flow
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:0fd875ff-914e-4a35-aafe-65127c1c2bdd
tags: []
subdomain: null
module: null
sensitivity: normal
name: ToC Add funds 出款充值端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
ToC Add funds（出款充值）端到端流程，覆盖 Customer 通过 app-sdk 发起请求，经 cgs、cashdesk-api 完成鉴权与下单，再由 fundout → pfs-payment → payment → cmf 链路落地资金请求，最后由 Timer 驱动 cmf-task 批量调用 h2h 与 BANK 完成出款执行与查询。

## 步骤(跨系统)

**阶段 1：用户发起与下单（Customer → app-sdk → cgs → cashdesk-api → ...）**

- 1：Customer → app-sdk
- 1.1：app-sdk → cgs `/cashdesk/fundoutAuth`
  - 1.1.1：cgs → cashdesk-api
    - 1.1.1.1：cashdesk-api → grc-check-identity-provider `PaymentSessionQueryStub#paymentSessionQuery`
- 1.2：app-sdk → cgs `/cashdesk/verify`
  - 1.2.1：cgs → cashdesk-api
    - 1.2.1.1：cashdesk-api → cmf `CardTokenFacade#create`
    - 1.2.1.2：cashdesk-api → fundout `FundoutSimpleFacade#pay`
      - 1.2.1.2.1：fundout → pfs-payment `FundOutPaymentFacade#pay`
        - 1.2.1.2.1.1：pfs-payment → payment `PaymentFacade#pay`
          - 1.2.1.2.1.1.1：payment → cmf `FundRequestFacade#apply`
- 1.3：app-sdk ⇠ Customer (dashed return)：`apply success`

**阶段 2：批量请求执行（Timer 驱动出款落地银行）**

- 2：Timer → cmf-task：batch request job
  - 2.1：cmf-task → h2h
    - 2.1.1：h2h → BANK

**阶段 3：批量查询（Timer 驱动状态回查）**

- 3：Timer → cmf-task：batch query job
  - 3.1：cmf-task → （后续接收方原文截断）

## 涉及服务/表
- 服务：app-sdk、cgs、cashdesk-api、fundout、pfs-payment、payment、grc-check-identity-provider、cmf、cmf-task、h2h、BANK
- 接口：
  - `/cashdesk/fundoutAuth`
  - `/cashdesk/verify`
  - `PaymentSessionQueryStub#paymentSessionQuery`
  - `CardTokenFacade#create`
  - `FundoutSimpleFacade#pay`
  - `FundOutPaymentFacade#pay`
  - `PaymentFacade#pay`
  - `FundRequestFacade#apply`
- 表：原文未提及

## 校验点
- 鉴权阶段：`/cashdesk/fundoutAuth` 须经 grc-check-identity-provider 的 `paymentSessionQuery` 校验。
- 下单阶段：`/cashdesk/verify` 触发 `CardTokenFacade#create` 与 `FundoutSimpleFacade#pay`，最终落到 cmf 的 `FundRequestFacade#apply`，apply success 后才返回 Customer。
- 执行阶段：cmf-task 通过 Timer 触发 batch request job，经 h2h 推送至 BANK。
- 查询阶段：cmf-task 通过 Timer 触发 batch query job 进行状态回查。
