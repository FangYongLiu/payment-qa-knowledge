---
id: domain_lending
object_type: Domain
name: lending
aliases: [quantix, SME Lending, BNPL, Pay Later, 信贷, 先买后付]
domain: lending
product: payment
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
dev_owner: xiaopei.yan
last_reviewed_at: '2026-06-26'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [lending, 信贷, BNPL, paylater]
related_services: [svc_botim_snpl, svc_paylater, svc_botim_credit, svc_credit_business, svc_cbm, svc_cqm, svc_youstore_installment]
---

# lending(借贷 / 先买后付)

> 域入口。SME Lending / BNPL 业务。owner / 研发 Quantix 团队(Xiaopei Yan)。("quantix" 是团队名,业务是 lending。)

## 概述
面向用户与商户的信贷能力:先买后付(SNPL / paylater)、信用分期、商户信用退款(credit-business)、Visa 交易转分期(TTS)、youstore 分期等。

## 本域内容
- **service/** — botim-snpl、paylater、botim-credit、credit-business、cbm、cqm、youstore-installment。

## 相邻域
分期卡发卡 → [[domain_card]];交易核心 → [[domain_payment_core]];风控 → [[domain_risk]]。
