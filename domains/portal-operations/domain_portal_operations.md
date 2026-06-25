---
id: domain_portal_operations
object_type: Domain
name: portal-operations
aliases: [门户/运营]
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [portal-operations, 门户/运营]
related_services: [svc_basis, svc_merchant, svc_hive_activities, svc_hive_bank_console, svc_hive_cashier, svc_hive_checkout, svc_hive_developers, svc_hive_m_topay, svc_hive_mcashier, svc_hive_merchant_console, svc_hive_portal, svc_hive_utilities, svc_merchant_frontend, svc_contract, svc_invoice, svc_basis_merchant, svc_corporate_portal, svc_unified_merchant_portal, svc_onboarding, svc_cregister, svc_basis_portal, svc_basis_cas]
---

# portal-operations(门户/运营)

> 业务域总览(入口节点)。owner yijian.tan。细节见各服务对象。

## 概述
门户与运营域:Hive 门户系列、商户门户(merchant/unified-merchant-portal)、基础门户(basis/basis-portal/basis-cas)、合同发票、商户入驻(onboarding)等运营侧能力。

## 覆盖范围
共 22 个服务:basis、merchant、hive-activities、hive-bank-console、hive-cashier、hive-checkout、hive-developers、hive-m-topay、hive-mcashier、hive-merchant-console、hive-portal、hive-utilities、merchant-frontend、contract、invoice、basis-merchant、corporate-portal、unified-merchant-portal、onboarding、cregister、basis-portal、basis-cas。

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[flow_acquire_product_application]](流程:收单商户控台产品申请与开通流程)
- [[flow_merchant_onboarding]](流程:商户注册与入驻端到端流程(Acquire + WPS))
- [[flow_mpgs_manual_onboarding]](流程:MPGS 手动报备(人工录入)入驻流程)
- [[scn_merchant_fee_bearer_separation]](场景:收支分离商户配置(独立 MID 扣手续费))
- [[scn_merchant_settlement_withdraw_auth]](场景:商户控台结算/提现/退款的双人授权)
- [[scn_onboarding_manual_register]](场景:MPGS 供应商人工录入报备)
