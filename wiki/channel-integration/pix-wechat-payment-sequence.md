---
title: pix-wechat微信支付时序流程
domain: channel-integration
kind: wiki_page
slug: pix-wechat-payment-sequence
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:76eac41d-bb5d-4022-b93a-793bc6d1e501
tags: []
---

# pix-wechat微信支付时序流程

本页描述 pix-wechat 渠道下微信扫码支付的端到端时序：用户发起交易 → 调起厂商扫码 → 创建收银台交易 → 异步收到支付成功 → 处理结果、通知厂商并落库对账。

## 参与组件

- **pix**：发起方（用户/上游）
- **pix-wechat**：微信支付渠道服务（核心编排）
- **tradeii**：收银台交易服务
- **query**：交易结果查询/接收组件
- **reconciliation**：对账服务
- **vendor (Tenpay)**：财付通/微信支付厂商侧

## 创建交易阶段

1. `MpcFacade.createTrade`：pix → pix-wechat 发起创建交易
2. 在 pix-wechat 内部并行/顺序执行：
   - 1.1 `scan code for payment`：pix-wechat → vendor (Tenpay) 调起扫码支付
   - 1.2 `CashierTradeFacade#createCashierTrade`：pix-wechat → tradeii 创建收银台交易
3. 1.3 pix-wechat 异步返回 pix（虚线返回，无附加报文）

## 支付结果处理阶段

待用户完成扫码支付后，由 query 组件接收到支付成功事件并驱动后续处理：

- 2 `trade success`：query 收到交易成功（自激活）
- 2.1 `process result`：query → pix-wechat，触发结果处理
- pix-wechat 在结果处理中依次执行：
  - 2.1.1 `notify payment result`：pix-wechat → vendor (Tenpay)，回调通知支付结果
  - 2.1.2 `save bill`：pix-wechat → reconciliation，落库账单用于对账
  - 2.1.3 `save glide`：pix-wechat → vendor (Tenpay)，保存 glide 记录

## 关键交互要点

- 创建交易与支付结果处理为两段独立活动，中间由用户扫码完成动作衔接
- pix-wechat 同时承担调起厂商、创建收银台交易、结果分发、对账落库等编排职责
- 结果链路由 query 触发，pix-wechat 串行完成厂商通知与对账双写

> 引用来源：wiki page `pix-RA-2405-STP-Wechat` 中的时序图（image-20240531-064223.png）
