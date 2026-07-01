---
id: scn_remittance_cross_border
object_type: Scenario
name: 跨境汇款 (Remittance)
aliases: []
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [remittance, 支付, cgs-apitest]
related_services: [svc_remittance, svc_cashierii, svc_tradeii, svc_payment, svc_member]
related_tables: []
related_logs: []
---

# 跨境汇款 (Remittance)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toC 跨境汇款:收款人管理(增改删/共享)、发起人信息、报价(quote)、确认汇款(confirm/sendNow)、重发,以及 VAM 虚拟账户。经 remittance 核心 + 收银支付。

## 关联关系
- **涉及服务**:[[svc_remittance]]、[[svc_cashierii]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:待补

## 校验点(QA)
- 收款人增改删/共享;quote 报价 + confirm/sendNow。
- 国家币种列表;发起人/收款人字段采集。
- VAM 虚拟账户查询;落库汇款单。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
