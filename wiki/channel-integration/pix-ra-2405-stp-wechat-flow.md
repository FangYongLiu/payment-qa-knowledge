---
title: pix-RA-2405-STP-Wechat 微信扫码支付流程
domain: channel-integration
kind: wiki_page
slug: pix-ra-2405-stp-wechat-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:2b437675-e3d9-4319-8cbe-f2a767763899
tags: []
---

# pix-RA-2405-STP-Wechat 微信扫码支付流程

描述用户通过 wallet 发起 WeChat/Tenpay 扫码支付时，wallet、cgs、pix、tradeii、bill 与 vendor(Tenpay) 之间的两阶段交互时序。端到端业务流程见 [[flow_pix_wechat_scan_payment]]。

## 参与方

- User：发起支付的用户
- wallet：钱包前端/收银台入口
- cgs：渠道网关
- pix：渠道集成核心组件（本流程焦点）
- tradeii：收银交易服务
- bill：账单服务
- vendor(Tenpay)：微信/财付通侧

## 阶段一：确认交易并展示收银台

由用户确认交易信息触发，wallet 通过 cgs 调用 pix，由 pix 同时向 Tenpay 申请扫码码与在 tradeii 创建收银台交易，最终回到 wallet 展示收银台。

1. User → wallet：`confirm trade information`
2. wallet → cgs：`/pix/mpc/v1/create-trade`
3. cgs → pix：（转发调用）
4. pix → vendor(Tenpay)：`scan code for payment`
5. pix → tradeii：`CashierTradeFacade#createCashierTrade`
6. pix → cgs：返回
7. cgs → wallet：返回
8. wallet → wallet：`show cashier`（自调用）
9. wallet → User：返回

## 阶段二：支付结果处理

用户完成支付后，由 Tenpay 侧驱动结果回传，pix 负责回执通知与账单落库。

1. User → wallet：`payment process`
2. vendor(Tenpay) → tradeii：`trade success`
3. tradeii → pix：`process result`
4. pix → vendor(Tenpay)：`notify payment result`
5. pix → bill：`save bill`

## 关键接口与方法

- `/pix/mpc/v1/create-trade`：wallet 经 cgs 创建交易的入口
- `CashierTradeFacade#createCashierTrade`：pix 调用 tradeii 创建收银台交易
- `scan code for payment`：pix 向 Tenpay 申请扫码码
- `notify payment result`：pix 回执 Tenpay 支付结果
- `save bill`：pix 通知 bill 落账
