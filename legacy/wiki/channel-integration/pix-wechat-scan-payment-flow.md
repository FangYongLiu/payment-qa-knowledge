---
title: pix-wechat WeChat扫码支付时序流程
domain: channel-integration
kind: wiki_page
slug: pix-wechat-scan-payment-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:18caca10-dace-474f-bf66-7ae48357e46a
tags: []
---

# pix-wechat WeChat扫码支付时序流程

本页描述 pix-wechat 作为编排核心，串联用户、Tenpay、tradeii、query、reconciliation 各方完成 WeChat 扫码支付的两阶段时序。

## 参与方

- pix（用户/发起方）
- pix-wechat（编排核心）
- tradeii（交易/账单）
- query（交易状态轮询）
- reconciliation（对账）
- vendor：Tenpay

## 阶段一：同步解析码与创建收银台交易

由用户侧发起，pix-wechat 顺序协调下游：

- 1: `MpcFacade.parseCode` — pix → pix-wechat
- 1.1: scan code for payment — pix-wechat → Tenpay
- 1.2: `CashierTradeFacade#createCashierTrade` — pix-wechat → tradeii
- 1.3: 返回（dashed）— pix-wechat → pix

## 阶段二：异步支付结果处理

由 query 检测到交易成功后触发，pix-wechat 再次被激活并扇出三路落库/通知：

- 2: trade success — query 自循环（activation）
- 2.1: process result — query → pix-wechat
- 2.1.1: notify payment result — pix-wechat → Tenpay
- 2.1.2: save bill — pix-wechat → tradeii
- 2.1.3: save glide — pix-wechat → reconciliation（对账单 glide 落库）

## 编排要点

- pix-wechat 是中心编排者，两个阶段均由其对外扇出调用。
- 阶段一为同步链路：解析码 → 调用 Tenpay 扫码 → 创建收银台交易 → 同步返回用户。
- 阶段二为异步链路：query 探测到成功后回调 pix-wechat，由其完成 Tenpay 结果通知、账单（bill）与对账记录（glide）的持久化。
