---
id: flow_cko_subscription_payment
object_type: Flow
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:7f45d807-e19a-4881-b2b6-39437be81a26
tags:
- CKO
- subscription
- MIT
- frictionless
subdomain: null
module: null
sensitivity: normal
name: CKO渠道订阅支付时序流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

CKO渠道订阅支付的端到端时序流程，由 User 发起，经 cgs->cashierii 编排，串联 authpay、grc、checkout、cmf、trade 等服务。流程分为两个主阶段：Confirm card payment（确认支付，处理授权、协议、风控）与 Verify card payment（验证支付，保存卡信息并确认支付）。

补充：在 cashdesk → cmf → router → qpay-cko → Checkout 的免3DS MIT Unscheduled 代扣链路中，cmf 通过 querySubscriptionChannel/FundIn 调 routerFacade 路由到 CKO 渠道，再由 qpay-cko 用已签 token 向 Checkout 提交 MIT Unscheduled 代扣。

## 步骤(跨系统)

### 1. Confirm card payment (User → cgs->cashierii)

- 1.1 Query auth pay perferSign：cgs->cashierii → authpay
- 1.2 Authorize result (perferSign)：authpay → cgs->cashierii

当 `preferSign=Y` 时进入以下分支：

- 1.3 Query sign protocol list：cgs->cashierii → grc
- 1.4 Signed protocols：grc → cgs->cashierii
- 1.5 Preroute for card payment channel with signed protocols：cgs->cashierii → checkout
- 1.6 Protocol whether available (frictionless)：checkout → cgs->cashierii
- 1.7 Payment event with frictionless：cgs->cashierii → authpay
  - 1.7.1 Save env infor：authpay self-call
  - 1.7.2 3ds：authpay → cgs->cashierii
- 1.8 Cache context：cgs->cashierii self-call
- 1.9 Risk result：cgs->cashierii → User

### 2. Verify card payment (User → cgs->cashierii)

- 2.1 Process preferSign and frictionless args：cgs->cashierii self-call
- 2.2 Save card information with preferSign or frictionless：cgs->cashierii → cmf
- 2.3 Card token id：cmf → cgs->cashierii
- 2.4 Confirm pay：cgs->cashierii → trade
  - 2.4.1 trade → cmf

### 3. querySubscriptionChannel 路由判定 (cashdesk → cmf)

- 1: querySubscriptionChannel {firctionless=Y, is3ds=N, signedSource=CKO,MC,xxx}：cashdesk → cmf
  - 1.1: routerFacade.preRoute：cmf → router
  - 1.2: channel=CKO111：router → cmf
- alt 分支：
  - [routeResponse.channel == null] 1.3: available = false：cmf → cashdesk
  - [routeResponse.channel != null] 1.4: available = true：cmf → cashdesk

### 4. 免3DS MIT Unscheduled 代扣 submit 链路 (cashdesk → payment → cmf → qpay-cko → Checkout)

- 2: pay {firctionless=Y, is3ds=N, signedSource=CKO,MC,xxx}：cashdesk → payment
  - 2.1: FundIn {firctionless=Y, is3ds=N, signedSource=CKO,MC,xxx}：payment → cmf
    - 2.1.1: routerFacade.route：cmf → router
    - 2.1.2: channel=CKO111：router → cmf
    - 2.1.3: apiType=DB：cmf → qpay-cko
      - 2.1.3.1: queryCardTokenByCardId：qpay-cko → member
      - 2.1.3.2: signedTransactionId：member → qpay-cko
      - 2.1.3.3: submit payment {previous_payment_id=xxx, payment_type=Unscheduled, merchant_initiated=true}：qpay-cko → Checkout
- 3: submit success：Checkout → qpay-cko
  - 3.1: query transaction：qpay-cko → Checkout

## 涉及服务/表

- cgs->cashierii：流程编排入口，缓存上下文，处理 preferSign 与 frictionless 参数
- authpay：查询 perferSign、保存环境信息、3ds、支付事件处理
- grc：查询并返回已签署协议列表
- checkout：根据已签协议进行 card payment 渠道预路由，判定 frictionless 是否可用
- cmf：保存卡信息、返回 card token id；承接 querySubscriptionChannel/FundIn，调用 routerFacade.preRoute / routerFacade.route，分发到 qpay-cko；并被 trade 回调
- trade：执行 confirm pay
- router：执行 routerFacade.preRoute / routerFacade.route，返回 channel（如 CKO111）
- qpay-cko：apiType=DB 入口，调 member 的 queryCardTokenByCardId 取 signedTransactionId，向 Checkout 提交 MIT Unscheduled 代扣并 query transaction
- member：提供 queryCardTokenByCardId，返回 signedTransactionId
- Checkout：CKO 收单方，接收 submit payment（previous_payment_id、payment_type=Unscheduled、merchant_initiated=true）
- cashdesk、payment：发起 querySubscriptionChannel 与 pay/FundIn

## 校验点

- 1.2 中 authpay 返回的 perferSign 决定是否进入签约分支（preferSign=Y）
- 1.6 checkout 返回的 frictionless 标识是否可用，影响 1.7 Payment event 与 2.2 Save card information 的处理路径
- 2.1 cgs->cashierii 需对 preferSign 与 frictionless 参数进行处理后再保存卡信息（2.2）与 confirm pay（2.4）
- querySubscriptionChannel 路由判定：以 routeResponse.channel 是否为 null 决定 available=false/true 返回给 cashdesk
- FundIn 入参须携带 firctionless=Y、is3ds=N、signedSource，路由命中 channel=CKO111 后进入 apiType=DB
- qpay-cko 提交 Checkout 时必须携带 previous_payment_id、payment_type=Unscheduled、merchant_initiated=true，对应免3DS 的 MIT Unscheduled 代扣语义
- signedTransactionId 由 member.queryCardTokenByCardId 返回，作为代扣 token 来源
