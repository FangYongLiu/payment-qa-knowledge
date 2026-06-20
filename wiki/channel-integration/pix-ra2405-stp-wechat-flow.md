---
title: PIX RA-2405 STP微信扫码支付流程
domain: channel-integration
kind: wiki_page
slug: pix-ra2405-stp-wechat-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e9a7ea72-7ef1-4850-a1f7-45e0d5cefc80
tags: []
---

# PIX RA-2405 STP微信扫码支付流程

本页描述微信/Tenpay 扫码支付（STP）从用户在 wallet 端发起下单、收银台展示，到 vendor 异步回调支付结果、并完成账单与对账数据落库的端到端时序。完整时序图见 [[flow_pix_wechat_stp_payment]]。

## 参与方（Lifelines）

- **User**：发起支付的终端用户
- **wallet**：钱包前端/客户端，承载收银台
- **cgs**：网关层，对外暴露 `/pix/mpc/*` 接口
- **pix**：支付核心域（本流程主控）
- **tradeii**：交易/账单持久化服务
- **query**：异步支付结果接收/查询服务
- **reconciliation**：对账（glide）落库服务
- **vendor**：Tenpay（微信支付）

## 下单与收银台展示

1. User → wallet：`confirm trade information`（确认交易信息）
2. wallet → cgs：`/pix/mpc/v1/create-trade`
3. cgs → pix：转发创建交易请求
4. pix → vendor(Tenpay)：`scan code for payment`（向 Tenpay 发起扫码下单）
5. pix → tradeii：`CashierTradeFacade#createCashierTrade`（创建收银台交易）
6. pix → cgs → wallet：返回结果
7. wallet：`show cashier`（展示收银台）
8. wallet → User：返回收银台

## 支付与异步结果通知

1. User → wallet：`payment process`（用户在收银台完成支付）
2. vendor(Tenpay) → query：`trade success`（Tenpay 异步通知支付成功）
3. query → pix：`process result`（处理支付结果）
4. pix 侧后续动作：
   - pix → vendor(Tenpay)：`notify payment result`
   - pix → tradeii：`save bill`（保存账单）
   - pix → reconciliation：`save glide`（写入对账记录）

## 状态确认（Wallet 侧）

1. wallet：`query mpc order`（自查 mpc 订单）
2. wallet → cgs：`/pix/mpc/v1/confirm-trade-status`
3. cgs → pix：转发状态确认请求

## 关键接口与方法

- `/pix/mpc/v1/create-trade`：创建 mpc 交易
- `/pix/mpc/v1/confirm-trade-status`：确认交易状态
- `CashierTradeFacade#createCashierTrade`：tradeii 收银台交易创建入口

## 关键持久化动作

- `save bill` → tradeii：账单落库
- `save glide` → reconciliation：对账数据落库
