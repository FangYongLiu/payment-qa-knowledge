---
id: flow_wallet_send_money
object_type: Flow
domain: payby-core-systems
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:93a9ab2a-3e50-434f-9328-e4fd1fa497ca
tags:
- send-money
- wallet
- transfer
- cashier
subdomain: wallet
module: transfer
sensitivity: normal
name: 钱包Send Money转账端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
钱包改版 Send Money 转账端到端流程：Payer 通过 cgs/transfer 进行最近转账查询、发送页初始化和发起转账；cgs/transfer 编排订单保存并委托 tradeii 创建 cashier trade，tradeii 调用 cgs/cashierii 创建并返回 pay token；token 回传至 Payer 后，Payer 直接调用 cgs/cashierii 完成支付。

## 步骤(跨系统)
1. `/wallet/transfer/v1/query-recent-sent`：Payer → cgs/transfer
   - 1.1 Recent transfers：cgs/transfer ⇢ Payer
2. `/wallet/transfer/v1/init-send-page`：Payer → cgs/transfer
   - 2.1 Page configuration：cgs/transfer ⇢ Payer
3. `/wallet/transfer/v1/send-money`：Payer → cgs/transfer
   - 3.1 Save order：cgs/transfer 自调用
   - 3.2 Create cashier trade：cgs/transfer → tradeii
     - 3.2.1 Create cashier token：tradeii → cgs/cashierii
     - 3.2.2 Pay token：cgs/cashierii ⇢ tradeii
   - 3.3 (返回)：tradeii ⇢ cgs/transfer
   - 3.4 Pay token：cgs/transfer ⇢ Payer
4. Pay：Payer → cgs/cashierii (直接调用，绕过 cgs/transfer 与 tradeii)
   - 4.1 Pay result：cgs/cashierii ⇢ Payer

## 涉及服务/表
- 服务：cgs/transfer、tradeii、cgs/cashierii
- 接口：
  - `/wallet/transfer/v1/query-recent-sent`
  - `/wallet/transfer/v1/init-send-page`
  - `/wallet/transfer/v1/send-money`
- 关键产物：cashier trade、pay token

## 校验点
- 步骤 3.1 Save order 在 cgs/transfer 内完成订单保存后，再触发 3.2 创建 cashier trade
- pay token 由 cgs/cashierii 生成，经 tradeii → cgs/transfer 透传至 Payer
- 最终 Pay 由 Payer 直接调用 cgs/cashierii，cgs/transfer 与 tradeii 不参与支付执行
- Pay result 由 cgs/cashierii 直接返回 Payer
