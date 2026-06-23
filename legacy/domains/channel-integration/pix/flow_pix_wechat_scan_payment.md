---
id: flow_pix_wechat_scan_payment
object_type: Flow
domain: channel-integration
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:fd3750e9-7e0a-4f24-ae38-9100b02bfaad
tags:
- pix
- wechat
- scan-payment
- cashier
subdomain: pix
module: mpc
sensitivity: normal
name: PIX WeChat扫码支付端到端流程
aliases: []
related_services: []
related_tables: []
related_scenarios:
- pix-ra-2405-stp-wechat-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
PIX渠道下WeChat扫码支付（STP）端到端时序流程。以wallet为客户端入口，cgs作为网关路由到pix编排器，pix对接外部vendor（Tenpay）完成扫码支付、创建收银台交易，并在交易成功后回调通知、落库账单与对账记录。来源：wiki页面 pix-RA-2405-STP-Wechat。

## 步骤(跨系统)
1. User → wallet：confirm trade information（用户确认交易信息）
   - 1.1 wallet → cgs：`POST /pix/mpc/v1/create-trade`
     - 1.1.1 cgs → pix：转发调用
       - 1.1.1.1 pix → vendor(Tenpay)：scan code for payment（扫码支付）
       - 1.1.1.2 pix → tradeii：`CashierTradeFacade#createCashierTrade`
       - 1.1.1.3 pix → cgs：返回
     - 1.2 cgs → wallet：返回
   - 1.3 wallet → wallet：show cashier（展示收银台）
   - 1.4 wallet → User：返回
2. User → wallet：payment process（发起支付）
3. query → tradeii：trade success（交易成功）
   - 3.1 tradeii → pix：process result
     - 3.1.1 pix → vendor(Tenpay)：notify payment result（通知支付结果）
     - 3.1.2 pix → query：save bill（落库账单）
     - 3.1.3 pix → reconciliation：save glide（对账落库）
4. wallet → wallet：query mpc order（查询MPC订单）
   - 4.1 wallet → cgs：`POST /pix/mpc/v1/confirm-trade-status`
     - 4.1.1 cgs → pix：转发调用

## 涉及服务/表
- 服务/参与方：User、wallet、cgs（网关）、pix（中心编排，highlighted）、tradeii、query、reconciliation、vendor(Tenpay)
- 接口：
  - `/pix/mpc/v1/create-trade`
  - `/pix/mpc/v1/confirm-trade-status`
  - `CashierTradeFacade#createCashierTrade`
- 外部交互：Tenpay 扫码支付、Tenpay 支付结果通知

## 校验点
- create-trade 阶段：pix须同时完成 Tenpay scan code 与 tradeii createCashierTrade
- 支付结果回调：tradeii→pix→Tenpay notify、query save bill、reconciliation save glide 三动作齐全
- wallet 通过 confirm-trade-status 轮询/确认 mpc 订单状态
- cgs仅作路由，pix为编排中心
