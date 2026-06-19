---
id: flow_cko_subscription_payment
object_type: Flow
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:3f710267-e8aa-4813-924f-3baaadc592a9
tags:
- 3DS
- subscription
- CKO
- preferSign
subdomain: cko
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

补充3DS订阅支付时序细节：当 `preferSign=Y` 且 `is3ds=Y` 时，cmf 通过 routeFacade.router 进行渠道路由，根据签约3ds渠道是否可用，分别走 CKO102（签约3ds渠道）或 MC101（普通3ds渠道）分支，最终通过 PAGE_URL 回传 H5 完成跳转，再由用户输入密码经 fcw 校验完成 challenge。

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

### 3. 3DS订阅支付时序（pay 链路，preferSign=Y, is3ds=Y）

- 1: pay — Actor2 → H5
- 1.1: pay — H5 → cashdesk
- 1.1.1: pay (preferSign=Y, is3ds=Y) — cashdesk → payment
- 1.1.1.1: FundIn (preferSign=Y, is3ds=Y) — payment → cmf
- 1.1.1.1.1: routeFacade.router — cmf → router

alt 路由分支：

- [签约3ds渠道可用] 1.1.1.1.2: channel=签约3ds渠道 (CKO102)
- [签约3ds渠道不可用] 1.1.1.1.3: channel=普通3ds渠道 (MC101)

后续（普通3ds渠道分支）：

- 1.1.1.1.3.1: apiType=DB — cmf → qpay-xxx渠道
- 1.1.1.1.3.2: channelResult {PAGE_URL} — qpay-xxx渠道 → cmf
- 1.1.1.1.3.3: cmfResult {PAGE_URL} — cmf → payment
- 1.1.1.1.3.3.1: PAGE_URL — payment → cashdesk
- 1.1.1.1.3.3.1.1: PAGE_URL — cashdesk → H5
- 1.1.1.1.3.3.1.1.1: redirect to PAGE_URL — H5 自跳转

密码校验（challenge）：

- 2: input password — Actor2 → H5
- 2.1: validate password — H5 → fcw
- 2.1.1: challenge success — fcw → member

## 涉及服务/表

- cgs->cashierii：流程编排入口，缓存上下文，处理 preferSign 与 frictionless 参数
- authpay：查询 perferSign、保存环境信息、3ds、支付事件处理
- grc：查询并返回已签署协议列表
- checkout：根据已签协议进行 card payment 渠道预路由，判定 frictionless 是否可用
- cashdesk：收银台，转发 pay 请求并回传 PAGE_URL 给 H5
- payment：支付服务，触发 FundIn 并向 cashdesk 回传 PAGE_URL
- cmf：保存卡信息、返回 card token id，被 trade 回调；通过 routeFacade.router 路由到具体渠道，封装 channelResult 为 cmfResult
- router：渠道路由，分流到 CKO102（签约3ds渠道）或 MC101（普通3ds渠道）
- qpay-xxx渠道：执行 apiType=DB 的渠道交易并返回 PAGE_URL
- fcw：校验用户密码，回传 challenge success
- trade：执行 confirm pay
- member：作为 lifeline 出现，接收 challenge success

## 校验点

- 1.2 中 authpay 返回的 perferSign 决定是否进入签约分支（preferSign=Y）
- 1.6 checkout 返回的 frictionless 标识是否可用，影响 1.7 Payment event 与 2.2 Save card information 的处理路径
- 2.1 cgs->cashierii 需对 preferSign 与 frictionless 参数进行处理后再保存卡信息（2.2）与 confirm pay（2.4）
- 1.1.1.1.1 路由结果决定渠道：签约3ds渠道可用 → CKO102；不可用 → MC101
- 普通3ds渠道分支以 apiType=DB 调用渠道，必须返回 PAGE_URL，并沿 cmf → payment → cashdesk → H5 链路逐级回传，最终由 H5 redirect to PAGE_URL
- 用户在 H5 输入密码后，由 fcw 校验并返回 challenge success 至 member
