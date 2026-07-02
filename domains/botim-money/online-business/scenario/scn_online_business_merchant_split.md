---
id: scn_online_business_merchant_split
object_type: Scenario
name: 商户分账 (Merchant Split)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [online-business, 支付, cgs-apitest]
related_services: [svc_tradeii, svc_payment, svc_pfs_payment, svc_merchant]
related_tables: []
related_logs: []
---

# 商户分账 (Merchant Split)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 商户分账:一笔交易按规则分账到多个商户,含分账退款(refundSharingAmount)。经 tradeii/payment + pfs 清分。

## 关联关系
- **涉及服务**:[[svc_tradeii]]、[[svc_payment]]、[[svc_pfs_payment]]、[[svc_merchant]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:待补

## 校验点(QA)
- 分账金额拆分正确;分账退款 refundSharingAmount。
- 各分账方落账;免登收银缓存卡支付路径。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
