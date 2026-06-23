---
title: Pix-Wechat支付时序流程
domain: channel-integration
kind: wiki_page
slug: pix-wechat-payment-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:1265ae6d-76af-46a7-b8a2-011abf08c917
tags: []
---

# Pix-Wechat支付时序流程

Pix 渠道经 wallet → cgs → pix 编排，调用 Tenpay 完成扫码支付，并将结果回写至 tradeii、bill、reconciliation。

## 参与方

- **User**：发起方
- **wallet**：客户端入口
- **cgs**：网关，转发请求至 pix
- **pix**：中心编排者（核心）
- **tradeii**：交易服务
- **bill**：账单服务
- **reconciliation**：对账服务
- **vendor**：Tenpay（微信支付）

## 阶段一：建单与收银台展示

1. User → wallet：confirm trade information
2. wallet → cgs：`/pix/mpc/v1/create-trade`
3. cgs → pix：转发调用
4. pix → vendor(Tenpay)：scan code for payment（扫码支付）
5. pix → tradeii：`CashierTradeFacade#createCashierTrade`
6. pix → cgs → wallet：逐层返回
7. wallet：show cashier（自调用渲染收银台）
8. wallet → User：返回展示

## 阶段二：支付与结果回写

1. User → wallet：payment process
2. vendor(Tenpay) → tradeii：trade success（支付成功通知）
3. tradeii → pix：process result
4. pix → vendor(Tenpay)：notify payment result
5. pix → bill：save bill
6. pix → reconciliation：save glide

## 关键说明

- 流程分为 **建单（1.x）** 与 **结果处理（3.x）** 两阶段
- pix 作为编排者贯穿全流程：对外联动 Tenpay，对内协同 tradeii / bill / reconciliation
- cgs 仅承担网关转发职责，不含业务编排
