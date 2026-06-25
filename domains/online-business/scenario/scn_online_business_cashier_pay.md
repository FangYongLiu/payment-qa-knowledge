---
id: scn_online_business_cashier_pay
object_type: Scenario
name: 收银台支付 (Cashier / PayPage)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [online-business, 支付, cgs-apitest]
related_services: [svc_cashierii, svc_acquireii, svc_tradeii, svc_payment, svc_member, svc_cards]
related_tables: []
related_logs: []
---

# 收银台支付 (Cashier / PayPage)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 收银台/受理面支付:BPG PayPage(免登/unauth 收银)、动态二维码、付款码、智慧码、智能POS、出租车、支付链接等多种受理形态。经 cashierii 收银核心 + acquireii 下单 → tradeii/payment。

## 关联关系
- **涉及服务**:[[svc_cashierii]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:见各 [[auto_*]](由 auto 的 `related_scenarios` 指向本场景)
- **读写的表**:待补

## 校验点(QA)
- 收银台 initTrade→confirmPay→queryResult 全链;免登(unauth)缓存卡/卡token支付/删支付方式。
- 余额/绑新卡/银行卡 多支付方式;退款。
- 各受理形态(POS/QR/智慧码/打车)的下单与回调一致性。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
