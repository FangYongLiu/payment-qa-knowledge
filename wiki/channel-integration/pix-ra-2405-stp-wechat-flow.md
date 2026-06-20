---
title: pix-RA-2405-STP WeChat扫码支付时序流程
domain: channel-integration
kind: wiki_page
slug: pix-ra-2405-stp-wechat-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:97449460-1dcb-46d5-bbbf-0ab1fffdec76
tags: []
---

# pix-RA-2405-STP WeChat扫码支付时序流程

本页描述 WeChat (Tenpay) 扫码支付的端到端调用时序，覆盖从用户确认交易到支付结果回调入账的完整链路。

## 参与方

时序图涉及以下 lifeline（自左至右）：

- User：发起支付的用户
- wallet：钱包前端/客户端
- cgs：渠道网关服务
- pix：渠道集成核心服务（流程主导方）
- tradeii：收银台/交易服务
- bill：账单存储服务
- vendor(Tenpay)：微信支付（财付通）外部渠道

## 创建交易阶段

用户确认交易信息后，自上而下依次发起调用：

1. User → wallet：confirm trade information
2. wallet → cgs：调用 `/pix/mpc/v1/create-trade`
3. cgs → pix：转发创建交易请求
4. pix → vendor(Tenpay)：scan code for payment（向微信请求扫码下单）
5. pix → tradeii：调用 `CashierTradeFacade#createCashierTrade` 创建收银台交易
6. pix → cgs → wallet：逐层返回结果
7. wallet 自调用：show cashier（向用户展示收银台）
8. wallet → User：返回展示完成

## 支付与结果通知阶段

用户在收银台完成支付动作后，结果由渠道异步回流：

1. User → wallet：payment process（用户执行支付）
2. vendor(Tenpay) → tradeii：trade success（微信通知交易成功）
3. tradeii → pix：process result（转交结果处理）
4. pix → vendor(Tenpay)：notify payment result（回执/通知支付结果）
5. pix → bill：save bill（持久化账单记录）

## 关键路径说明

- 创建交易方向：wallet → cgs → pix，pix 同时与 vendor 和 tradeii 交互。
- 结果回调方向：vendor(Tenpay) → tradeii → pix，pix 负责回执 vendor 并落库到 bill。
- pix 在整条链路中作为主导编排方，负责对接外部渠道与内部交易/账单系统。
