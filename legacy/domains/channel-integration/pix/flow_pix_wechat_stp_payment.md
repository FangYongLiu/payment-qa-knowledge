---
id: flow_pix_wechat_stp_payment
object_type: Flow
domain: channel-integration
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:e9a7ea72-7ef1-4850-a1f7-45e0d5cefc80
tags:
- pix
- wechat
- stp
- tenpay
- scan-code
subdomain: pix
module: stp-wechat
sensitivity: normal
name: PIX微信STP扫码支付端到端流程
aliases: []
related_services:
- wallet
- cgs
- pix
- tradeii
- query
- reconciliation
related_tables: []
related_scenarios:
- pix-ra2405-stp-wechat-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

PIX RA-2405 STP 微信(Tenpay)扫码支付端到端流程：用户在 wallet 确认交易后，wallet 经 cgs 调用 pix 发起扫码支付，pix 向 vendor(Tenpay)申请扫码并在 tradeii 创建收银台交易；展示收银台后用户完成支付，vendor 异步将支付成功结果回调至 query，再由 query 转交 pix 处理(通知 vendor、落库 tradeii、写入 reconciliation)；最后 wallet 通过 cgs→pix 确认交易状态。

## 步骤(跨系统)

1. User → wallet：confirm trade information
   - 1.1 wallet → cgs：`/pix/mpc/v1/create-trade`
     - 1.1.1 cgs → pix：创建交易
       - 1.1.1.1 pix → vendor(Tenpay)：scan code for payment(扫码支付申请)
       - 1.1.1.2 pix → tradeii：`CashierTradeFacade#createCashierTrade`
       - 1.1.1.3 pix → cgs：返回
     - 1.2 cgs → wallet：返回
   - 1.3 wallet：show cashier(展示收银台)
   - 1.4 wallet → User：返回

2. User → wallet：payment process(用户完成支付)

3. vendor(Tenpay) → query：trade success(异步成功通知)
   - 3.1 query → pix：process result
     - 3.1.1 pix → vendor(Tenpay)：notify payment result
     - 3.1.2 pix → tradeii：save bill
     - 3.1.3 pix → reconciliation：save glide

4. wallet：query mpc order(自查订单)

5. wallet → cgs：`/pix/mpc/v1/confirm-trade-status`
   - 5.1 cgs → pix：确认交易状态

## 涉及服务/表

- 服务：wallet、cgs、pix、tradeii、query、reconciliation、vendor(Tenpay)
- 接口：`/pix/mpc/v1/create-trade`、`/pix/mpc/v1/confirm-trade-status`、`CashierTradeFacade#createCashierTrade`
- 数据落地：tradeii(bill)、reconciliation(glide)

## 校验点

- 创建交易链路：wallet→cgs→pix→vendor 扫码 + tradeii 创建收银台交易是否成功
- 收银台展示与返回链路是否完整(1.3 / 1.4)
- 异步回调路径：vendor→query→pix 的支付结果处理
- pix 处理结果时三件事是否齐全：通知 vendor(notify payment result)、tradeii 落 bill、reconciliation 落 glide
- 最终一致性：wallet 通过 `/pix/mpc/v1/confirm-trade-status` 经 cgs→pix 确认交易状态
