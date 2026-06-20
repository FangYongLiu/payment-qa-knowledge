---
id: flow_cko_subscription_payment
object_type: Flow
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:1d01c9fc-0178-4a06-8ef9-eae6975bca3b
tags:
- CKO
- subscription
- 3DS
- preferSign
- frictionless
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

CKO渠道订阅支付的端到端时序流程，由 User 发起，经 cgs->cashierii 编排，串联 authpay、grc、member、checkout、cmf、trade 等服务。流程分为两个主阶段：Confirm card payment（确认支付：授权预查、协议匹配、预路由、风控）与 Verify card payment（验证支付：保存卡信息、Pay and Sign、3ds form 返回）。Lifelines 顺序：User、cgs->cashierii、grc、member、authpay、trade、cmf、checkout。

## 步骤(跨系统)

### 1. Confirm card payment (User → cgs->cashierii)

- 1.1 Query auth pay perferSign：cashierii → authpay
- 1.2 Authorize result (perferSign)：authpay → cashierii

当 `preferSign=Y` 时进入以下分支（frame: preferSign=Y）：

- 1.3 Query sign protocol list：cashierii → member
- 1.4 Signed protocols：member → cashierii
- 1.5 Preroute for card payment channel with signed protocols：cashierii → checkout
- 1.6 Protocol whether available (frictionless)：checkout → cashierii

分支结束后继续：

- 1.7 Payment event with frictionless：cashierii → grc
  - 1.7.1 Save env infor：grc self-call
  - 1.7.2 3ds：grc → cashierii
- 1.8 Cache context：cashierii self-call
- 1.9 Risk result：cashierii → User

### 2. Verify card payment (User → cashierii)

- 2.1 Process preferSign and frictionless args：cashierii self-call
- 2.2 Save card information with preferSign or frictionless：cashierii → cmf
- 2.3 Card token id：cmf → cashierii
- 2.4 Confirm pay：cashierii → trade
  - 2.4.1 trade → cmf
    - 2.4.1.1 Pay and Sign：cmf → checkout
      - 2.4.1.2 checkout → cmf
  - 2.4.2 cmf → trade
- 2.5 3ds form：trade → cashierii

## 涉及服务/表

- cgs->cashierii：流程编排入口；处理 preferSign 与 frictionless 参数；缓存上下文（Cache context）
- authpay：返回 Authorize result 中的 perferSign 标识
- member：提供已签署协议列表（sign protocol list / Signed protocols）
- checkout：基于已签协议进行 card payment 渠道预路由，判定 frictionless 是否可用；承接 Pay and Sign
- grc：处理 Payment event with frictionless，保存 env infor，返回 3ds
- cmf：保存卡信息并返回 card token id；被 trade 回调，向 checkout 发起 Pay and Sign
- trade：执行 Confirm pay，回调 cmf，最终返回 3ds form

## 校验点

- 1.2 authpay 返回的 perferSign 是分支判断条件，仅 preferSign=Y 才进入 1.3–1.6 协议查询与预路由分支
- 1.6 checkout 返回的 frictionless 标识决定 1.7 Payment event 是否带 frictionless，并影响 2.2 Save card information 的存储路径
- 2.1 cashierii 必须先对 preferSign 与 frictionless 参数进行处理，再执行 2.2 保存卡信息
- 2.4.1.1 Pay and Sign 由 cmf 调用 checkout 完成，是订阅支付（Pay + Sign 合一）的关键调用
- 2.5 trade 最终返回 3ds form 给 cashierii，作为 Verify 阶段的结果
