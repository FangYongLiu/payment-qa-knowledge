---
title: PIX渠道WeChat扫码支付时序流程
domain: channel-integration
kind: wiki_page
slug: pix-ra-2405-stp-wechat-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:fd3750e9-7e0a-4f24-ae38-9100b02bfaad
tags: []
---

# PIX渠道WeChat扫码支付时序流程

本页描述 PIX RA-2405 场景下，用户通过 WeChat 扫码完成支付的端到端时序，涵盖收银台创建、支付处理、结果通知与订单状态确认。相关端到端视角见 [[flow_pix_wechat_scan_payment]]。

## 参与方

- **User**：发起支付的用户（actor）
- **wallet**：客户端入口
- **cgs**：网关，负责路由到 pix
- **pix**：核心编排方（流程中枢）
- **tradeii**：交易服务（CashierTrade）
- **query**：查询/账单服务
- **reconciliation**：对账服务
- **vendor (Tenpay)**：外部渠道方（WeChat/财付通）

## 阶段一：确认交易并创建收银台

1. User → wallet：confirm trade information
2. wallet → cgs：`/pix/mpc/v1/create-trade`
3. cgs → pix：转发调用
4. pix → vendor (Tenpay)：scan code for payment（扫码支付）
5. pix → tradeii：`CashierTradeFacade#createCashierTrade`
6. pix → cgs：返回
7. cgs → wallet：返回
8. wallet 自调用：show cashier（展示收银台）
9. wallet → User：返回

## 阶段二：用户完成支付

- User → wallet：payment process（用户在收银台完成支付动作）

## 阶段三：支付结果回调与落库

1. query → tradeii：trade success
2. tradeii → pix：process result
3. pix 后续动作并行展开：
   - pix → vendor (Tenpay)：notify payment result（通知支付结果）
   - pix → query：save bill（保存账单）
   - pix → reconciliation：save glide（保存对账数据）

## 阶段四：MPC订单状态确认

1. wallet 自调用：query mpc order
2. wallet → cgs：`/pix/mpc/v1/confirm-trade-status`
3. cgs → pix：转发调用

## 关键说明

- **wallet** 是客户端入口；**cgs** 仅作网关转发；**pix** 是被高亮的中枢编排方，负责与外部渠道 Tenpay 交互、创建收银台交易、保存账单与对账数据。
- 创建交易接口：`/pix/mpc/v1/create-trade`
- 状态确认接口：`/pix/mpc/v1/confirm-trade-status`
- 交易创建依赖：`CashierTradeFacade#createCashierTrade`
