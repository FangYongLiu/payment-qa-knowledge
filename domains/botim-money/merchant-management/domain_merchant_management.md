---
id: domain_merchant_management
object_type: Domain
name: merchant-management
aliases: [portal-operations, 商户管理, 门户/运营, merchant-portal, cs-portal]
domain: merchant-management
business_line: botim-money
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
- **api/**(4)· **flow/**(3)· **scenario/**(4,含 [[scn_merchant_portal_registration]] 门户自助注册向导)。

## 相邻域
收单交易 → [[domain_online_business]] / [[domain_offline_business]];出款(平台侧)→ [[domain_fundout]];工资代发 → [[domain_wps]](同为 Chahid 团队)。

## 服务索引
- **商户核心 / 运营后台**:[[svc_merchant]]、[[svc_basis_merchant]]、[[svc_contract]]、[[svc_invoice]]、[[svc_onboarding]]、[[svc_cregister]]、[[svc_merchant_fundout]]。
- **门户 / 控台**:[[svc_unified_merchant_portal]]、[[svc_merchant_frontend]]、[[svc_corporate_portal]](企业 Portal)、[[svc_hive_merchant_console]] 及 hive 控台子应用 [[svc_hive_portal]] / [[svc_hive_cashier]] / [[svc_hive_checkout]] / [[svc_hive_developers]] / [[svc_hive_activities]] / [[svc_hive_bank_console]] / [[svc_hive_m_topay]] / [[svc_hive_utilities]]。
- **客服**:[[svc_customer_service]]。

## 参考索引
- [[reference_merchant_portal_overview]](Merchant Portal 商户控台总览 —— 控台权威总览)
- [[reference_merchant_management_overview]](商户管理总览 —— 域级)
- [[reference_bmoc_basis_merchant_overview]](BMOC Basis Merchant 运营后台模块)
- [[reference_device_activation_overview]](设备激活流程 / Smart POS)
- [[reference_wps_knowledge_base_overview]](WPS 知识库总览)
- [[reference_wps_payroll_qa_onboarding]](WPS Payroll QA 入职计划)
- [[reference_qa_standards_overview]](QA 规范总览)
