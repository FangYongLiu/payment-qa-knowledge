---
id: scn_wallet_deposit
object_type: Scenario
name: 钱包充值 (Deposit / Top-Up)
aliases: []
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [wallet, 支付, cgs-apitest]
related_services: [svc_cashierii, svc_member, svc_tradeii, svc_payment, svc_cards]
related_tables: []
related_logs: []
---

# 钱包充值 (Deposit / Top-Up)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toC 钱包充值:KYC 用户绑卡/已绑卡充值、Kiosk 网点充值(KYC/Non-KYC)、新收银台充值;含账户异常/未KYC/KYC过期 异常分支。

## 关联关系
- **涉及服务**:[[svc_cashierii]]、[[svc_member]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cards]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:见各 [[auto_*]](由 auto 的 `related_scenarios` 指向本场景)
- **读写的表**:待补

## 校验点(QA)
- 绑卡+充值、已绑卡充值;新/旧收银台路径。
- 异常:账户状态异常(E301)、未KYC(E302)、KYC过期(E303)。
- 充值限额 getLimitation;落库充值单。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
