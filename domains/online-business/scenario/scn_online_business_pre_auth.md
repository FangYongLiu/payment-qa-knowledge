---
id: scn_online_business_pre_auth
object_type: Scenario
name: 预授权 / 请款 (PreAuth-Capture)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [online-business, 支付, cgs-apitest]
related_services: [svc_acquireii, svc_tradeii, svc_payment, svc_cards, svc_acs]
related_tables: []
related_logs: []
---

# 预授权 / 请款 (PreAuth-Capture)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 预授权-请款:绑卡/卡token(MOTO 带/不带CVV)预授权 → 撤销(Void)/部分请款(Capture)/(部分)退款,含 3DS 降级。

## 关联关系
- **涉及服务**:[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]]、[[svc_acs]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:待补

## 校验点(QA)
- 预授权 → Void / 部分 Capture / 全额·部分退款 状态流转。
- MOTO CVV/NoCVV 分支;3DS 降级(N108)。
- refund_pay_voucher_no 与 captured 金额一致。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
