---
id: scn_wallet_withdraw
object_type: Scenario
name: 钱包提现 (Withdraw)
aliases: []
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [wallet, 支付, cgs-apitest]
related_services: [svc_member, svc_tradeii, svc_payment, svc_pfs_payment]
related_tables: []
related_logs: []
---

# 钱包提现 (Withdraw)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toC 钱包提现:KYC/VIP/VVIP 用户提现到已绑卡或新绑 IBAN。

## 关联关系
- **涉及服务**:[[svc_member]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_pfs_payment]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:见各 [[auto_*]](由 auto 的 `related_scenarios` 指向本场景)
- **读写的表**:待补

## 校验点(QA)
- 已绑卡 vs 新绑 IBAN 提现;不同会员等级(KYC/VIP/VVIP)额度。
- withdraw_init → withdraw 流程;落库提现单。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
