---
id: flow_cko_subscription_payment
object_type: Flow
domain: channel-integration
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:67db0de7-529a-47fd-bc0d-b41af9edeb6d
tags:
- CKO
- 订阅支付
- 时序图
- preferSign
- frictionless
- 3DS
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

CKO渠道订阅支付的端到端时序流程，由 User 发起，经 cgs->cashierii 编排，串联 authpay、grc、member、checkout、cmf、trade 等服务。流程分为两个主阶段：Confirm card payment（确认支付，处理授权 perferSign、查询签约协议、预路由与风控3DS）与 Verify card payment（验证支付，保存卡 Token 并执行 PayAndSign 确认支付）。

## 步骤(跨系统)

Lifelines: User、cgs->cashierii、grc、member、authpay、trade、cmf、checkout。

### 1. Confirm card payment (User → cgs->cashierii)

- 1.1 Query auth pay perferSign：cashierii → authpay
- 1.2 Authorize result (perferSign)：authpay → cashierii

当 `preferSign=Y` 时进入分支(frame: preferSign=Y)：

- 1.3 Query sign protocol list：cashierii → member
- 1.4 Signed protocols：member → cashierii
- 1.5 Preroute for card payment channel with signed protocols：cashierii → checkout
- 1.6 Protocol whether available (frictionless)：checkout → cashierii

后续步骤（不限于 preferSign=Y 分支）：

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

- cgs->cashierii：流程编排入口，缓存上下文 (Cache context)，处理 preferSign 与 frictionless 参数
- authpay：查询 perferSign，返回 Authorize result
- member：返回已签署协议列表 (Signed protocols)
- checkout：基于已签协议进行 card payment 渠道预路由，判定 Protocol whether available (frictionless)，并承接 Pay and Sign 调用
- grc：处理 Payment event with frictionless，保存环境信息 (Save env infor)、执行 3ds
- cmf：保存卡信息并返回 Card token id；在 Confirm pay 链路中被 trade 调用，再向 checkout 发起 Pay and Sign
- trade：执行 Confirm pay，返回 3ds form

## 校验点

- 1.2 中 authpay 返回的 perferSign 决定是否进入签约分支（frame: preferSign=Y）
- 1.6 checkout 返回的 frictionless 标识是否可用，影响 1.7 Payment event with frictionless 的处理与后续 2.2 Save card information 的入参
- 2.1 cashierii 需对 preferSign 与 frictionless 参数进行处理后再保存卡信息 (2.2) 与 Confirm pay (2.4)
- 2.4.1.1 Pay and Sign 由 cmf 调用 checkout 完成支付与签约联动
- 2.5 trade 返回 3ds form 给 cashierii，作为验证支付阶段的最终输出
