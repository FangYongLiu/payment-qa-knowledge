---
title: CKO渠道订阅支付流程
domain: payby-authorization-protocol
kind: wiki_page
slug: cko-channel-subscription-payment-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:85ed1b71-c6cd-4173-8bad-a92dae660154
tags: []
---

# CKO渠道订阅支付流程

本页描述 CKO 渠道下，用户发起绑卡到完成 3DS 验证并签约的端到端时序交互，涵盖前端、会员域、收银台、风控、CMF 与 checkout 之间的协作。

## 参与方

- **User**：发起绑卡与签约的终端用户
- **personal**：用户侧个人中心入口
- **member-front**：会员前置服务
- **member**：会员核心服务
- **cashdesk**：收银台
- **grc**：风控
- **cmf**：支付中台/卡管理
- **checkout**：CKO 渠道收单方

## 流程概览

整体分为两个顶层交互：

1. **保存卡 + 发起支付**：返回 3DS 表单给用户
2. **用户验证签约**：由 checkout 触达后，回传结果并激活卡

## 阶段一：Save card 与 3DS 表单下发

1. `Save card`：User → personal
   - 1.1 `Process card`：personal → member-front
     - 1.1.1 `Save member card`：member-front → member
     - 1.1.2 member 返回
     - 1.1.3 `Risk Non-Payment event`：member-front → grc（风控非支付事件）
     - 1.1.4 grc 返回
     - 1.1.5 `Save card token`：member-front → cmf
     - 1.1.6 `Card token id`：cmf → member-front
     - 1.1.7 `Pay`：member-front → cmf
       - 1.1.7.1 `Pay and sign`：cmf → checkout
       - 1.1.7.2 checkout 返回
     - 1.1.8 `3ds form`：cmf → member-front
   - 1.2 member-front 返回 personal
   - 1.3 `3ds form`：personal → User

## 阶段二：Verify and sign 与签约结果回传

2. `Verify and sign`：User → checkout
   - 2.1 checkout 返回 User
   - 2.2 `Sign protocol data`：checkout → cmf
     - 2.2.1 `Save and relate data`：cmf 自调用，保存并关联签约数据
     - 2.2.2 `Accept bind card result`：cmf → cashdesk
       - 2.2.2.1 `Activate card with sign channel`：cashdesk → member（按签约渠道激活卡）
       - 2.2.2.2 `Notify grc card success`：cashdesk → grc（通知风控绑卡成功）

## 关键说明

- 卡 token 在 cmf 侧落库后再发起 `Pay and sign`，由 checkout 返回 3DS 表单
- 用户在 checkout 上完成 3DS 验证后，由 checkout 主动回调 cmf 进行协议数据签约
- 绑卡成功的最终态由 cashdesk 串联：先在 member 激活卡并标记签约渠道，再向 grc 通知成功

## 相关

- 流程图详见 [[flow_cko_subscription_payment]]
