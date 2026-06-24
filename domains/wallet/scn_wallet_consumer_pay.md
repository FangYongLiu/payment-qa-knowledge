---
id: scn_wallet_consumer_pay
object_type: Scenario
name: 消费者付款 (Payment Code / PPC)
aliases: []
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [wallet, 支付, cgs-apitest]
related_services: [svc_tradeii, svc_payment, svc_member, svc_cashierii]
related_tables: []
related_logs: []
---

# 消费者付款 (Payment Code / PPC)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toC 消费者付款:付款码支付、PPC 交易(含预授权/提现等多形态,45 TC)。

## 关联关系
- **涉及服务**:[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cashierii]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:见各 [[auto_*]](由 auto 的 `related_scenarios` 指向本场景)
- **读写的表**:待补

## 校验点(QA)
- 付款码生成与扣款;PPC 各交易形态(preAuth/withdraw 等)。
- 退款金额;落库。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
