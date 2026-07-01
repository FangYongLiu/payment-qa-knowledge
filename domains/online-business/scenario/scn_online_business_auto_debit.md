---
id: scn_online_business_auto_debit
object_type: Scenario
name: 自动代扣 / 签约 (Auto Debit)
aliases: []
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [online-business, 支付, cgs-apitest]
related_services: [svc_authpay, svc_deduct, svc_tradeii, svc_payment, svc_member, svc_cards]
related_tables: []
related_logs: []
---

# 自动代扣 / 签约 (Auto Debit)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toB 自动代扣:基于签约(sign_contract_no)+ 代扣渠道(deductChannelId)用余额/银行卡/余额+卡组合扣款,含扣款失败与退款。经 authpay 授权 + deduct 执行 → tradeii/payment。

## 关联关系
- **涉及服务**:[[svc_authpay]]、[[svc_deduct]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_member]]、[[svc_cards]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:待补

## 校验点(QA)
- 余额/银行卡/组合扣款成功与失败(N104/105)分支。
- 签约 contract_no 有效性;deductChannelId 路由。
- 扣款后退款;落库扣款单状态。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
