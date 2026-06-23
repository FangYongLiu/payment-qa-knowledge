---
title: Wallet Redesign - Send Money 转账流程
domain: remittance
kind: wiki_page
slug: wallet-redesign-send-money-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9f0c0a0d-1a4b-4e72-b124-d44b671ddd00
tags: []
---

# Wallet Redesign - Send Money 转账流程

本页基于时序图描述 Wallet 改版后 Send Money 的端到端交互链路，以及根据收款人(Payee)状态分支触发的通知方式。

## 参与方

- Botim message window：消息窗入口
- Payer：付款人
- cashier：收银台
- tradeii：交易系统
- cgs/transfer：转账核心
- pns：站内消息通知服务
- mns：短信通知服务
- Payee：收款人

## 主流程时序

1. Botim message window → Payer：进入 Send Money (Enter send money)
2. Payer → Payer：Send (本地确认)
3. Payer → cashier：Pay
   - 3.1 cashier → tradeii：Pay
     - 3.1.1 tradeii 自处理：Pay
     - 3.1.2 tradeii → cgs/transfer：Notice payment result
       - 3.1.2.1 cgs/transfer 自处理：Update order

## 收款人通知分支

cgs/transfer 在更新订单后，根据 Payee 状态进入下列三个 `sd` 备选片段之一：

### Registered with KYC（已注册并完成 KYC）

- 3.1.2.2 cgs/transfer → pns：Message window notification
- 3.1.2.2.1 pns → Payee：Received

### Registered without KYC（已注册但未完成 KYC）

- 3.1.2.3 cgs/transfer → pns：Message window notification
- 3.1.2.3.1 pns → Payee：Receiving

### Unregistered（未注册）

- 3.1.2.4 cgs/transfer → mns：Sms notification
- 3.1.2.4.1 mns → Payee：Receive remind

## 通知通道差异

- 已注册用户(无论是否 KYC)：通过 pns 推送站内消息窗通知
- 已 KYC vs 未 KYC：到账文案差异为 Received(已入账) / Receiving(待领取/处理中)
- 未注册用户：通过 mns 走短信通道发送 Receive remind 提醒

## 相关链接

- 端到端流程图与节点说明参见 [[flow_send_money]]

</br>
*注：原文末尾包含一个未完整描述的 loop 片段，本页未涵盖。*
