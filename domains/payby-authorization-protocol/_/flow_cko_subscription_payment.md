---
id: flow_cko_subscription_payment
object_type: Flow
domain: payby-authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki_image
source_ref: wiki_image:bea17c38-8186-48b8-af81-72e06ea7ec56
tags:
- CKO
- 订阅支付
- 时序图
- preferSign
- frictionless
subdomain: null
module: null
sensitivity: normal
name: CKO渠道订阅支付时序流程
aliases: []
related_services:
- cashierii
- authpay
- grc
- member
- checkout
- cmf
- trade
related_tables: []
related_scenarios:
- cko-channel-subscription-payment-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

CKO渠道订阅支付的端到端时序流程，由 User 发起，经 cgs->cashierii 编排，串联 authpay、grc、checkout、cmf、trade 等服务。流程分为两个主阶段：Confirm card payment（确认支付，处理授权、协议、风控）与 Verify card payment（验证支付，保存卡信息并确认支付）。

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

## 涉及服务/表

- cgs->cashierii：流程编排入口，缓存上下文，处理 preferSign 与 frictionless 参数
- authpay：查询 perferSign、保存环境信息、3ds、支付事件处理
- grc：查询并返回已签署协议列表
- checkout：根据已签协议进行 card payment 渠道预路由，判定 frictionless 是否可用
- cmf：保存卡信息、返回 card token id，并被 trade 回调
- trade：执行 confirm pay
- member：作为 lifeline 出现

## 校验点

- 1.2 中 authpay 返回的 perferSign 决定是否进入签约分支（preferSign=Y）
- 1.6 checkout 返回的 frictionless 标识是否可用，影响 1.7 Payment event 与 2.2 Save card information 的处理路径
- 2.1 cgs->cashierii 需对 preferSign 与 frictionless 参数进行处理后再保存卡信息（2.2）与 confirm pay（2.4）
