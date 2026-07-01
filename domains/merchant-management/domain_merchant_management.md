---
id: domain_merchant_management
object_type: Domain
name: merchant-management
aliases: [portal-operations, 商户管理, 门户/运营, merchant-portal, cs-portal]
domain: merchant-management
product: payment
status: active
owner: yijian.tan
reviewer: yijian.tan
dev_owner: chahid.arid
last_reviewed_at: '2026-06-26'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [merchant-management, 商户管理, 门户, 运营后台]
related_services: [svc_merchant, svc_basis_merchant, svc_contract, svc_onboarding, svc_cregister, svc_invoice, svc_unified_merchant_portal, svc_merchant_frontend, svc_merchant_fundout, svc_agreements_static, svc_basis, svc_basis_portal, svc_hive_merchant_console, svc_hive_mcashier]
---

# merchant-management(商户管理与运营)

> 域入口。商户侧的入驻、门户、配置与运营后台。owner yijian.tan / 研发 Merchant Portal & Operations 团队(Chahid Arid)。

## 概述
商户从注册入驻到日常经营的管理平台,以及公司运营人员的审批后台。覆盖商户入驻(onboarding/客户注册/NI 入网)、商户门户与控台、合同/发票/费率配置、商户转账(merchant-fundout),以及 basis 运营后台(商户审批、产品配置、结算/WPS 企业运营)。收单交易本身在 online-business / offline-business。

## 本域内容
- **service/** — 商户核心 merchant、运营后台 basis/basis-merchant/basis-portal、门户 unified-merchant-portal/merchant-frontend/hive-*、合同 contract、发票 invoice、入驻 onboarding/cregister、商户出款 merchant-fundout、协议 agreements-static。
- **table/** — merchant、mhtfundout(商户出款)、onboarding。
- **api/**(4)· **flow/**(3)· **scenario/**(3)。

## 相邻域
收单交易 → [[domain_online_business]] / [[domain_offline_business]];出款(平台侧)→ [[domain_fundout]];工资代发 → [[domain_wps]](同为 Chahid 团队)。
