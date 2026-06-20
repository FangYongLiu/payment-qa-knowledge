---
title: PIX WeChat STP 创建交易时序
domain: channel-integration
kind: wiki_page
slug: pix-wechat-stp-create-trade-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:270fbf80-e31c-452a-be74-5788eda768a2
tags: []
---

# PIX WeChat STP 创建交易时序

本页描述 PIX-WeChat STP 集成中 create-trade 的调用链路，涵盖从用户确认交易到收银台展示的完整时序，以及各参与服务的职责。

## 参与方

- **User**：发起并确认交易的终端用户
- **wallet**：钱包前端/服务，负责收银台展示
- **cgs**：网关服务，暴露 create-trade 接口
- **pix**：核心处理服务（本流程焦点）
- **tradeii**：交易服务，负责创建收银台交易
- **vendor(Tenpay)**：微信支付（财付通）渠道侧

## 调用时序

按编号顺序列出消息（实线为同步调用，虚线为返回）：

1. `confirm trade information`：User → wallet
   1.1. `/pix/mpc/v1/create-trade`：wallet → cgs
      1.1.1. cgs → pix（转发调用）
         1.1.1.1. `scan code for payment`：pix → vendor(Tenpay)
         1.1.1.2. `CashierTradeFacade#createCashierTrade`：pix → tradeii
         1.1.1.3. pix → cgs（返回）
   1.2. cgs → wallet（返回）
   1.3. `show cashier`：wallet 自调用（展示收银台）
   1.4. wallet → User（返回）

## 各服务职责

- **wallet**：接收用户确认动作，调用 cgs 接口；最终在本地展示收银台 UI
- **cgs**：提供 `/pix/mpc/v1/create-trade` 入口，转发到 pix 并回传结果
- **pix**：流程核心，向下游同时驱动渠道扫码与交易创建
  - 调用 vendor(Tenpay) 完成 `scan code for payment`
  - 通过 `CashierTradeFacade#createCashierTrade` 调用 tradeii 创建收银台交易
- **tradeii**：通过 `CashierTradeFacade` 创建 cashier trade
- **vendor(Tenpay)**：微信支付渠道侧，处理扫码支付请求

## 关键接口

- 入口接口：`/pix/mpc/v1/create-trade`
- 内部 Facade：`CashierTradeFacade#createCashierTrade`
- 渠道动作：`scan code for payment`(vendor(Tenpay))
