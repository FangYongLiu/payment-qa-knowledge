---
title: ToC Add funds 端到端时序流程
domain: fund-out-transfer
kind: wiki_page
slug: toc-add-funds-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:0fd875ff-914e-4a35-aafe-65127c1c2bdd
tags: []
---

# ToC Add funds 端到端时序流程

本页描述 ToC 场景下 Add funds（出款充值）从 Customer 发起到 BANK 落地的完整时序，涉及 app-sdk、cgs、cashdesk-api、fundout、pfs-payment、payment、cmf、cmf-task、h2h 等服务协作。

## 参与方

- **Timer**：定时触发批处理任务
- **Customer**：发起充值的客户
- **app-sdk**：客户端 SDK
- **cgs**：网关服务
- **cashdesk-api**：收银台 API
- **fundout**：出款服务
- **pfs-payment**：支付服务
- **payment**：核心支付
- **grc-check-identity-provider**：身份校验
- **cmf**：资金管理（Cash Management Facility）
- **cmf-task**：cmf 批处理任务
- **h2h**：Host-to-Host 银行通道
- **BANK**：银行

## 阶段一：客户发起与支付申请（同步链路）

### 1.1 鉴权 `/cashdesk/fundoutAuth`

- Customer → app-sdk → cgs：调用 `/cashdesk/fundoutAuth`
- cgs → cashdesk-api
- cashdesk-api → grc-check-identity-provider：`PaymentSessionQueryStub#paymentSessionQuery`，进行支付会话身份校验

### 1.2 支付校验与申请 `/cashdesk/verify`

- Customer → app-sdk → cgs：调用 `/cashdesk/verify`
- cgs → cashdesk-api，cashdesk-api 内部依次发起：
  1. cashdesk-api → cmf：`CardTokenFacade#create`，创建卡 token
  2. cashdesk-api → fundout：`FundoutSimpleFacade#pay`
     - fundout → pfs-payment：`FundOutPaymentFacade#pay`
       - pfs-payment → payment：`PaymentFacade#pay`
         - payment → cmf：`FundRequestFacade#apply`，提交资金请求

### 1.3 同步返回

- app-sdk ⇠ Customer：返回 `apply success`（仅表示申请已受理，非最终银行结果）

## 阶段二：批处理请款（异步出账）

- Timer → cmf-task：触发 **batch request job**
- cmf-task → h2h
- h2h → BANK：将申请的资金请求批量送至银行

## 阶段三：批处理查询（异步对账）

- Timer → cmf-task：触发 **batch query job**
- cmf-task 后续向下游发起结果查询，回写银行处理状态

## 关联

- 流程定义见 [[flow_toc_add_funds]]
