---
id: scn_online_business_merchant_payout
object_type: Scenario
name: 商户出款 / 转账 (Transfer / Payout)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [online-business, 支付, cgs-apitest]
related_services: [svc_fundout, svc_merchant_fundout, svc_remittance, svc_tradeii, svc_payment, svc_cards]
related_tables: []
related_logs: []
---

# 商户出款 / 转账 (Transfer / Payout)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 出款/转账:转账下单(到手机号/TOTOK UID/公司MID/个人MID)、转账到银行(本币AED/USD、SWIFT USD)、转账到卡(个人/对公、卡资格校验、卡token)。经 fundout/merchant-fundout + remittance 通道。

## 关联关系
- **涉及服务**:[[svc_fundout]]、[[svc_merchant_fundout]]、[[svc_remittance]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:见各 [[auto_*]](由 auto 的 `related_scenarios` 指向本场景)
- **读写的表**:待补

## 校验点(QA)
- placeTransferOrder 各收款方类型;到银行 本币/SWIFT 币种与通道。
- 到卡资格校验(Standard/FastFunds);卡token 复用。
- 出款单状态与回调;落库。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
