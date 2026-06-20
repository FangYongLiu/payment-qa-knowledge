---
title: Pix-Wechat STP创建交易与收银台时序
domain: remittance
kind: wiki_page
slug: pix-ra-2405-stp-wechat-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:78fe06c4-b235-498e-aa74-b21e79667d80
tags: []
---

# Pix-Wechat STP创建交易与收银台时序

本页记录 Pix-Wechat 渠道（STP 场景）下，用户在 wallet 端确认交易后，经 cgs 转发到 pix，由 pix 协同 Tenpay 与 tradeii 完成扫码、本地金额计算与收银台交易创建的端到端调用时序。

## 参与方

- **User**：发起方用户
- **wallet**：客户端入口
- **cgs**：网关，负责把 wallet 的请求转发给 pix
- **pix**：核心编排组件（本流程焦点）
- **tradeii**：收银台交易服务
- **vendor(Tenpay)**：外部供应商，提供扫码支付能力

## 主流程时序

1. **User → wallet**：`confirm trade information`（用户确认交易信息）
   - 1.1 **wallet → cgs**：`/pix/mpc/v1/create-trade`
     - 1.1.1 **cgs → pix**：转发调用
       - 1.1.1.1 **pix → vendor(Tenpay)**：`scan code for payment`（扫码支付）
       - 1.1.1.2 **pix → pix**：`calculate local amount`（本地金额计算，自调用）
       - 1.1.1.3 **pix → tradeii**：`CashierTradeFacade#createCashierTrade`（创建收银台交易）
       - 1.1.1.4 **pix → cgs**：返回
     - 1.2 **cgs → wallet**：返回
   - 1.3 **wallet → wallet**：`show cashier`（展示收银台，自调用）
   - 1.4 **wallet → User**：返回
2. **User → wallet**：`complete cashier flow`（用户在收银台完成后续支付动作）

## 关键说明

- wallet 是客户端入口；cgs 作为网关只做转发，不承担业务编排。
- pix 在一次 `create-trade` 调用内串行完成三件事：
  1. 调用 Tenpay 扫码
  2. 本地金额换算
  3. 通过 `CashierTradeFacade#createCashierTrade` 在 tradeii 落地收银台交易
- 实线箭头为同步调用，虚线箭头为返回响应。
- 步骤 2 `complete cashier flow` 为收银台展示之后的用户后续动作，本时序图未展开其内部细节。
