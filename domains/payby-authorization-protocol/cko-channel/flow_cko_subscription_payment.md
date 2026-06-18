---
id: flow_cko_subscription_payment
object_type: Flow
domain: payby-authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki_image
source_ref: wiki_image:85ed1b71-c6cd-4173-8bad-a92dae660154
tags:
- CKO
- 订阅支付
- 签约
- 3DS
- 保存卡
subdomain: cko-channel
module: subscription-payment
sensitivity: normal
name: CKO渠道订阅支付签约流程
aliases: []
related_services:
- personal
- member-front
- member
- cashdesk
- grc
- cmf
- checkout
related_tables: []
related_scenarios:
- cko-channel-subscription-payment-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

CKO 渠道订阅支付签约流程描述用户通过 CKO 渠道完成保存卡、3DS 验证、签约协议并激活卡的端到端流程。流程包含两个顶层交互：(1) 保存卡并发起支付，返回 3DS 表单给用户；(2) 用户在 checkout 完成验证/签约，结果向下游传播以激活卡并通知风控。

## 步骤(跨系统)

**阶段 1：保存卡 + 发起支付 + 返回 3DS 表单**

- 1: Save card — User → personal
- 1.1: Process card — personal → member-front
  - 1.1.1: Save member card — member-front → member
  - 1.1.2: (return) — member → member-front
  - 1.1.3: Risk Non-Payment event — member-front → grc
  - 1.1.4: (return) — grc → member-front
  - 1.1.5: Save card token — member-front → cmf
  - 1.1.6: Card token id — cmf → member-front
  - 1.1.7: Pay — member-front → cmf
    - 1.1.7.1: Pay and sign — cmf → checkout
    - 1.1.7.2: (return) — checkout → cmf
  - 1.1.8: 3ds form — cmf → member-front
- 1.2: (return) — member-front → personal
- 1.3: 3ds form — personal → User

**阶段 2：用户验证签约 + 协议落库 + 卡激活**

- 2: Verify and sign — User → checkout
- 2.1: (return) — checkout → User
- 2.2: Sign protocol data — checkout → cmf
  - 2.2.1: Save and relate data — cmf 自调用
  - 2.2.2: Accept bind card result — cmf → cashdesk
    - 2.2.2.1: Activate card with sign channel — cashdesk → member
    - 2.2.2.2: Notify grc card success — cashdesk → grc

## 涉及服务/表

涉及服务：
- personal
- member-front
- member
- cashdesk
- grc
- cmf
- checkout

## 校验点

- 保存卡阶段需先在 member 落卡，再上报 grc 的 Risk Non-Payment 事件，随后在 cmf 保存 card token 并取得 card token id。
- 发起支付时由 cmf 调用 checkout 的 Pay and sign，返回 3ds form 经 member-front → personal 透传给 User。
- 用户在 checkout 完成 Verify and sign 后，checkout 通过 Sign protocol data 将协议数据回传 cmf。
- cmf 需 Save and relate data(协议数据落库与关联)，再通过 Accept bind card result 通知 cashdesk。
- cashdesk 必须执行 Activate card with sign channel(以签约渠道激活卡)并 Notify grc card success(通知风控签约/绑卡成功)。
