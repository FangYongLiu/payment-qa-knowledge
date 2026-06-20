---
id: flow_wallet_send_money
object_type: Flow
domain: payby-core-systems
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:99b17164-eac5-49be-88d1-780ad699d491
tags:
- send-money
- wallet
- cashier
- transfer
subdomain: wallet
module: transfer
sensitivity: normal
name: Wallet Send Money 端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios:
- wallet-redesign-send-money-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Wallet Redesign Send Money 端到端转账流程，覆盖 Payer 进入发送页、提交转账、由 cgs/transfer 编排下单、tradeii 创建收银交易、cgs/cashierii 生成 PayToken 并最终完成支付的全链路时序。涉及四个生命线：Payer、cgs/transfer、tradeii、cgs/cashierii。

## 步骤(跨系统)
1. **查询最近转账记录**
   - `1`: Payer → cgs/transfer  `/wallet/transfer/v1/query-recent-sent`
   - `1.1`: cgs/transfer ⇢ Payer  返回 Recent transfers

2. **初始化发送页**
   - `2`: Payer → cgs/transfer  `/wallet/transfer/v1/init-send-page`
   - `2.1`: cgs/transfer ⇢ Payer  返回 Page configuration

3. **提交转账下单(获取 PayToken)**
   - `3`: Payer → cgs/transfer  `/wallet/transfer/v1/send-money`
   - `3.1`: cgs/transfer 自调用 Save order(本地保存订单)
   - `3.2`: cgs/transfer → tradeii  Create cashier trade
     - `3.2.1`: tradeii → cgs/cashierii  Create cashier token
     - `3.2.2`: cgs/cashierii ⇢ tradeii  返回 Pay token
   - `3.3`: tradeii ⇢ cgs/transfer  返回(无显式标签)
   - `3.4`: cgs/transfer ⇢ Payer  返回 Pay token

4. **执行支付(Payer 直连 cashier)**
   - `4`: Payer → cgs/cashierii  Pay(绕过 cgs/transfer 与 tradeii)
   - `4.1`: cgs/cashierii ⇢ Payer  返回 Pay result

## 涉及服务/表
- 服务：
  - cgs/transfer：发送页编排、订单保存、收银交易创建调用入口
  - tradeii：创建 cashier trade，调用 cashierii 申请 PayToken
  - cgs/cashierii：创建 cashier token、签发 Pay token、执行 Pay 并返回结果
- 接口：
  - `/wallet/transfer/v1/query-recent-sent`
  - `/wallet/transfer/v1/init-send-page`
  - `/wallet/transfer/v1/send-money`
- 表：原文未提及。

## 校验点
- 步骤 3 中 `Save order` 必须先于 `Create cashier trade`(由 cgs/transfer 自调用完成)。
- PayToken 由 cgs/cashierii 生成，经 tradeii、cgs/transfer 透传至 Payer。
- 最终 Pay 调用由 Payer 直接发起到 cgs/cashierii，不经过 cgs/transfer 或 tradeii。
- 返回链路：cashierii → tradeii → cgs/transfer → Payer 必须完整传递 Pay token。
