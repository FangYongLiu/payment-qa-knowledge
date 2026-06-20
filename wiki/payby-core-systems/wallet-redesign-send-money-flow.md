---
title: 钱包改版 Send Money 转账流程
domain: payby-core-systems
kind: wiki_page
slug: wallet-redesign-send-money-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:93a9ab2a-3e50-434f-9328-e4fd1fa497ca
tags: []
---

# 钱包改版 Send Money 转账流程

本页描述钱包改版后 Send Money 场景下，从最近转账查询、页面初始化、下单到最终支付的端到端时序交互。

## 参与方

- **Payer**：发起转账的付款用户
- **cgs/transfer**：转账业务编排服务
- **tradeii**：交易服务
- **cgs/cashierii**：收银台服务

## 端到端时序

### 1. 查询最近转账记录

- `/wallet/transfer/v1/query-recent-sent`：Payer → cgs/transfer
- 返回 Recent transfers

### 2. 初始化转账页面

- `/wallet/transfer/v1/init-send-page`：Payer → cgs/transfer
- 返回 Page configuration

### 3. 提交转账下单

- `/wallet/transfer/v1/send-money`：Payer → cgs/transfer
- **3.1 Save order**：cgs/transfer 自身调用，保存订单
- **3.2 Create cashier trade**：cgs/transfer → tradeii，创建收银交易
  - **3.2.1 Create cashier token**：tradeii → cgs/cashierii，创建支付 token
  - **3.2.2 Pay token**：cgs/cashierii ⇢ tradeii，返回 pay token
- **3.3**：tradeii ⇢ cgs/transfer，返回结果
- **3.4 Pay token**：cgs/transfer ⇢ Payer，将 pay token 返回给前端

### 4. 发起支付

- **Pay**：Payer → cgs/cashierii，前端拿到 pay token 后**直接**调用收银台支付，绕过 cgs/transfer 与 tradeii
- **Pay result**：cgs/cashierii ⇢ Payer，返回支付结果

## 关键说明

- cgs/transfer 负责订单编排与保存，将收银交易创建委托给 tradeii。
- pay token 由 cgs/cashierii 生成，经 tradeii、cgs/transfer 透传给 Payer。
- 真正的支付动作由 Payer 直接发起到 cgs/cashierii，转账编排链路不再介入。

## 相关链接

- [[flow_wallet_send_money]]：完整端到端流程定义
