---
id: scn_channel_fund_in
object_type: Scenario
name: 渠道充值入金 (Fund-In)
aliases: []
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [channel, cgs-apitest]
related_services: [svc_qpay_cko, svc_qpay_mpgs, svc_acquireii, svc_tradeii, svc_payment]
related_tables: []
related_logs: []
---

# 渠道充值入金 (Fund-In)

> 业务测试场景。来源 cgs-apitest 回归。

## 场景描述
经第三方收单渠道(CKO / MPGS)充值入金(fundIn):卡支付入金、3DS、退款等。渠道(qpay-cko/mpgs)→ acquireii 下单 → tradeii/payment。

## 关联关系
- **涉及服务**:[[svc_qpay_cko]]、[[svc_qpay_mpgs]]、[[svc_acquireii]]、[[svc_tradeii]]、[[svc_payment]](= `related_services`)
- **覆盖的自动化**:见各 [[auto_*]]
- **读写的表**:待补

## 校验点(QA)
- CKO/MPGS 入金下单与回调;3DS 分支。
- 入金到账与退款;渠道返回码映射。
- 落库入金单状态。

## 来源与置信
- cgs-apitest 套件整理;服务链由调用线索+callgraph 推断,部分待补。
