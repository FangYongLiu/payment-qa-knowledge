---
title: Pix渠道WeChat/Tenpay扫码STP支付时序
domain: channel-integration
kind: wiki_page
slug: pix-wechat-stp-payment-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:71df4839-a93c-449c-b9b2-51255b04bb27
tags: []
---

# Pix渠道WeChat/Tenpay扫码STP支付时序

本页描述 Pix 渠道下 WeChat/Tenpay 扫码 STP 场景的支付时序，涵盖下单展示收银台、用户支付、以及异步结果回调三个阶段。

## 参与方

时序图中的 lifeline（从左到右）：

- User（用户）
- wallet
- cgs
- pix（核心处理方）
- tradeii
- query
- reconciliation
- vendor（Tenpay）

## 阶段一：下单与展示收银台

用户确认交易信息后，由 wallet 发起创建交易，最终回到 wallet 展示收银台。

- 1: User → wallet: `confirm trade information`
- 1.1: wallet → cgs: `/pix/mpc/v1/create-trade`
- 1.1.1: cgs → pix（调用）
  - 1.1.1.1: pix → vendor (Tenpay): `scan code for payment`
  - 1.1.1.2: pix → tradeii: `CashierTradeFacade#createCashierTrade`
  - 1.1.1.3: pix → cgs（返回）
- 1.2: cgs → wallet（返回）
- 1.3: wallet → wallet: `show cashier`（自调用）
- 1.4: wallet → User（返回）

## 阶段二：用户支付

- 2: User → wallet: `payment process`

由用户在收银台侧发起支付动作。

## 阶段三：异步交易成功回调

由 query 触发 trade success，经 tradeii 转发到 pix；pix 负责通知渠道结果、持久化账单并写入对账数据。

- 3: query → tradeii: `trade success`
- 3.1: tradeii → pix: `process result`
  - 3.1.1: pix → vendor (Tenpay): `notify payment result`
  - 3.1.2: pix → tradeii: `save bill`
  - 3.1.3: pix → reconciliation: `save glide`

## 关键关系小结

- 阶段一：wallet → cgs → pix 链路创建收银台交易，pix 同时调用 Tenpay 扫码与 tradeii 建单，再逐层返回展示收银台 UI。
- 阶段二：由用户主动发起支付。
- 阶段三：异步成功回调中，pix 是结果分发的中心节点，负责通知 vendor、保存账单（save bill）以及落地对账记录（save glide）。
