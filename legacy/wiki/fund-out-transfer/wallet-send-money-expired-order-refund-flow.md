---
title: Wallet Send Money 过期订单退款时序
domain: fund-out-transfer
kind: wiki_page
slug: wallet-send-money-expired-order-refund-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:5214a72e-c525-4bfe-b230-5185472dd68e
tags: []
---

# Wallet Send Money 过期订单退款时序

本页描述 Wallet Send Money 场景下，过期订单触发退款时 transfer、tradeii、pns 三方的交互时序（domain=fund-out-transfer）。

## 参与方

- **transfer**：编排方，负责扫描过期订单、发起退款、更新订单状态、触发通知。
- **tradeii**：退款执行方，接收 transfer 的退款发起请求并返回结果。
- **pns**：消息通知服务，向 payer 与 payee 推送 message window 通知。

## 时序步骤

1. **Query expired orders**：transfer 自身轮询/查询过期订单。
2. **Initiate refund**：transfer 同步调用 tradeii 发起退款。
   - 2.1：tradeii 同步返回退款结果给 transfer。
3. **Update order**：transfer 在本地更新订单状态。
4. **Message window notice payer and payee**：transfer 调用 pns，向 payer 与 payee 发送 message window 通知。

## 流程要点

- transfer 在整个流程中持续处于激活状态（步骤 1–4 全程编排）。
- tradeii 仅在步骤 2 / 2.1 期间激活，承担退款动作。
- pns 仅在步骤 4 激活，负责双向通知。
- 退款先于订单状态更新与通知；订单更新成功后才触发消息通知。
