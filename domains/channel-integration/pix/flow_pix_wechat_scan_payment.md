---
id: flow_pix_wechat_scan_payment
object_type: Flow
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:2b437675-e3d9-4319-8cbe-f2a767763899
tags:
- PIX
- WeChat
- Tenpay
- 扫码支付
- cashier
subdomain: pix
module: null
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
PIX 接入 Tenpay(WeChat) 扫码支付的端到端流程。用户在 wallet 确认交易后，经 cgs → pix 调用 Tenpay 获取扫码并在 tradeii 创建 cashier trade；用户完成支付后，Tenpay 回调 tradeii，再由 pix 通知支付结果并在 bill 落账单。

## 步骤(跨系统)
**Phase 1：创建交易并展示收银台**
1. User → wallet：confirm trade information
1.1 wallet → cgs：`/pix/mpc/v1/create-trade`
1.1.1 cgs → pix：(转发调用)
1.1.1.1 pix → vendor(Tenpay)：scan code for payment(获取扫码)
1.1.1.2 pix → tradeii：`CashierTradeFacade#createCashierTrade`
1.1.1.3 pix → cgs：返回
1.2 cgs → wallet：返回
1.3 wallet → wallet：show cashier(展示收银台)
1.4 wallet → User：返回

**Phase 2：支付与结果回调**
2. User → wallet：payment process(用户完成支付)
3. vendor(Tenpay) → tradeii：trade success
3.1 tradeii → pix：process result
3.1.1 pix → vendor(Tenpay)：notify payment result
3.1.2 pix → bill：save bill

## 涉及服务/表
- **服务/参与方**：wallet、cgs、pix、tradeii、bill、vendor(Tenpay)
- **关键接口**：
  - cgs 入口：`/pix/mpc/v1/create-trade`
  - tradeii：`CashierTradeFacade#createCashierTrade`
- **外部渠道**：Tenpay(WeChat 扫码支付)

## 校验点
- Phase 1 中 pix 同时完成「向 Tenpay 取扫码」与「在 tradeii 创建 cashier trade」两件事，缺一会导致收银台无法正常展示。
- `create-trade` 链路返回后 wallet 才能 show cashier；返回失败需阻断展示。
- Phase 2 由 Tenpay 主动回调 tradeii，再触发 pix 的 process result。
- pix 在收到结果后须：① 向 Tenpay `notify payment result`；② 向 bill `save bill`，两步顺序与完整性是落账正确性的关键校验点。
