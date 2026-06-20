---
title: Wallet Redesign Send Money 转账流程时序
domain: payby-core-systems
kind: wiki_page
slug: wallet-redesign-send-money-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:99b17164-eac5-49be-88d1-780ad699d491
tags: []
---

# Wallet Redesign Send Money 转账流程时序

本页描述 Wallet Redesign 场景下 Send Money 的端到端时序：从查询近期转账、初始化发送页，到下单并通过收银台完成支付。

## 参与方

- **Payer**：发起转账的用户
- **cgs/transfer**：转账编排服务
- **tradeii**：交易服务
- **cgs/cashierii**：收银台服务

## 端到端时序

### 1. 查询近期转账
- `1` Payer → cgs/transfer：`/wallet/transfer/v1/query-recent-sent`
- `1.1` cgs/transfer ⇢ Payer：返回 Recent transfers

### 2. 初始化发送页
- `2` Payer → cgs/transfer：`/wallet/transfer/v1/init-send-page`
- `2.1` cgs/transfer ⇢ Payer：返回 Page configuration

### 3. 下单并创建收银台交易
- `3` Payer → cgs/transfer：`/wallet/transfer/v1/send-money`
- `3.1` cgs/transfer 自调用：Save order
- `3.2` cgs/transfer → tradeii：Create cashier trade
  - `3.2.1` tradeii → cgs/cashierii：Create cashier token
  - `3.2.2` cgs/cashierii ⇢ tradeii：返回 Pay token
- `3.3` tradeii ⇢ cgs/transfer：返回（无标签）
- `3.4` cgs/transfer ⇢ Payer：返回 Pay token

### 4. 最终支付
- `4` Payer → cgs/cashierii：Pay（直接调用，绕过 cgs/transfer 与 tradeii）
- `4.1` cgs/cashierii ⇢ Payer：返回 Pay result

## 编排要点

- cgs/transfer 负责订单保存（Save order）与编排，将收银台交易创建委托给 tradeii。
- tradeii 调用 cgs/cashierii 生成 Pay token，并将其逐层回传至 Payer。
- 拿到 Pay token 后，Payer **直接**调用 cgs/cashierii 执行 Pay，不再经过 cgs/transfer 与 tradeii。

## 相关

- 完整端到端流程参见 [[flow_wallet_send_money]]。
