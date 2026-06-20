---
id: flow_send_money
object_type: Flow
domain: remittance
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:9f0c0a0d-1a4b-4e72-b124-d44b671ddd00
tags:
- send-money
- transfer
- sequence
subdomain: null
module: null
sensitivity: normal
name: Send Money 转账端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Send Money 转账端到端流程：Payer 在 Botim 消息窗口发起转账，经 cashier 收银台调用 tradeii 完成支付，tradeii 通知 cgs/transfer 更新订单，再由 cgs/transfer 根据 Payee 的注册及 KYC 状态，通过 pns（消息窗口通知）或 mns（短信通知）触达收款人。

## 步骤(跨系统)
1. Botim message window → Payer：Enter send money（进入转账入口）
2. Payer → Payer：Send（自身确认发送）
3. Payer → cashier：Pay
   - 3.1 cashier → tradeii：Pay
     - 3.1.1 tradeii → tradeii：Pay（内部支付处理）
     - 3.1.2 tradeii → cgs/transfer：Notice payment result
       - 3.1.2.1 cgs/transfer → cgs/transfer：Update order（更新订单）
       - 根据 Payee 状态进入以下三个互斥分支(sd)：
         - **Registered with KYC**：
           - 3.1.2.2 cgs/transfer → pns：Message window notification
           - 3.1.2.2.1 pns → Payee：Received
         - **Registered without KYC**：
           - 3.1.2.3 cgs/transfer → pns：Message window notification
           - 3.1.2.3.1 pns → Payee：Receiving
         - **Unregistered**：
           - 3.1.2.4 cgs/transfer → mns：Sms notification
           - 3.1.2.4.1 mns → Payee：Receive remind

## 涉及服务/表
- 服务/系统：
  - Botim message window（入口）
  - cashier（收银台，受理 Pay）
  - tradeii（支付处理，回传支付结果）
  - cgs/transfer（订单更新与通知编排）
  - pns（消息窗口通知通道）
  - mns（短信通知通道）
- 角色：Payer、Payee
- 表：原文未提供。

## 校验点
- Payer 在 Botim 消息窗口发起 Send Money，调用链：Payer → cashier → tradeii。
- tradeii 内部完成 Pay 后，必须 Notice payment result 给 cgs/transfer。
- cgs/transfer 收到结果后先 Update order，再按 Payee 状态分发通知，三个分支互斥：
  - Registered with KYC → pns，Payee 状态为 Received。
  - Registered without KYC → pns，Payee 状态为 Receiving。
  - Unregistered → mns，Payee 状态为 Receive remind。
- 注册且 KYC 与 注册未 KYC 均走 pns（消息窗口通知），区别在于 Payee 端最终态（Received vs Receiving）。
- 未注册用户仅通过 mns 短信触达，不走 pns。
