---
id: scn_wallet_p2p
object_type: Scenario
name: 钱包 P2P 转账 / 红包 (Transfer & Red Packet)
aliases: []
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: repo
source_ref: cgs-apitest/testcases/payment
tags: [wallet, 支付, cgs-apitest]
related_services: [svc_member, svc_tradeii, svc_payment, svc_cashierii]
related_tables: []
related_logs: []
---

# 钱包 P2P 转账 / 红包 (Transfer & Red Packet)

> 业务测试场景。来源 cgs-apitest 回归。穿过 payment-core 交易/支付核心。

## 场景描述
toC 个人间转账:手机号转账、好友转账(余额/银行卡支付)、AA 收款、红包(发/领/过期退回/Non-KYC 限制)。

## 关联关系
- **涉及服务**:[[svc_member]]、[[svc_tradeii]]、[[svc_payment]]、[[svc_cashierii]](= `related_services`,穿过的服务链)
- **覆盖的自动化**:由覆盖本场景的 AutomationAsset 在其 `related_scenarios` 中声明。
- **读写的表**:待补

## 校验点(QA)
- 余额/银行卡支付转账;收款方 KYC/Non-KYC 限制。
- 红包过期退回(E101)、Non-KYC 收发限制(E102/103);退款金额。
- AA 拆分收款;落库转账/红包单。

## 来源与置信
- cgs-apitest payment 套件整理;服务链由调用线索+callgraph 推断,部分标待补。
