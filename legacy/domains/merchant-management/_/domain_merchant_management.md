---
id: domain_merchant_management
object_type: Domain
domain: merchant-management
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:34ef57ae-73fe-4cd4-a064-e8edfb238167
tags:
- merchant
- onboarding
- acquire
- wps
subdomain: null
module: null
sensitivity: normal
name: 商户管理业务域
aliases: []
related_services: []
related_tables:
- merchant.t_merchant_creation_order
- merchant.t_merchant
- merchant.t_merchant_address
- merchant.t_partner
- merchant.t_binding_card_apply_info
- merchant.t_merchant_biz_open
- merchant.t_biz_admin_info
- merchant.t_merchant_acquire_info
- merchant.t_merchant_wps_info
- merchant.t_common_audit_order
- merchant.t_staff
- merchant.t_staff_role
- member.tm_member
- member.tm_member_identity
- member.tr_member_account
- member.tr_beneficiary_info
- ppcenter.t_product_apply_order
- ppcenter.t_merchant_product_order
- dpm.t_dpm_outer_account_subset
- statementii.t_settlement_config
- contract.t_contract
- vis.t_virtual_account
related_scenarios:
- merchant-registration-sources
- merchant-acquire-onboarding-flow
- merchant-wps-onboarding-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
商户管理业务域负责商户从注册申请到业务开通(Acquire / WPS)的端到端管理，覆盖申请受理、Basis 审核、会员与账户激活、产品/合同/对账配置等环节，并维护商户、会员、产品中心、账户、账单、合同、虚拟账户等多库的数据一致性。

## 覆盖范围
- 商户注册来源：Unified Portal、Agent、Basis、Botim
- 业务开通类型：Acquire、WPS
- 主数据库范围：
  - Merchant 商户库
  - Member 会员库
  - ppcenter 产品中心库
  - dpm 会员账户库
  - statementii 账单库
  - contract 合同库
  - vis 虚拟账户库
- 环境提示：UAT 环境下 Iban 需手动推进

## 关键服务/流程
### 1. Unified Portal 提交 Acquire 申请
- 接口：`/api/acquiring/permitAll/merchant/apply/add`
- 开通业务：Acquire 或 WPS
- 请求数据体：`acquireInfoList`、`addressList`、`bindingCard`、`bizAdminList`、`merchantData`、`partnerList`、`signatory`、`wpsInfoList`
- 写入数据：
  - merchant.t_merchant_creation_order 商户创建信息
  - merchant.t_merchant 商户信息
  - merchant.t_merchant_address 地址列表 `["register","business"]`
  - merchant.t_partner 合作伙伴
  - merchant.t_binding_card_apply_info 绑卡
  - merchant.t_merchant_biz_open 开通业务 `["Acquire","WPS"]`
  - merchant.t_biz_admin_info 业务管理员 `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
  - merchant.t_merchant_acquire_info Acquire 业务
  - merchant.t_staff、merchant.t_staff_role
  - member.tm_member（状态 0 未激活）、member.tm_member_identity（状态 0 未激活）

### 2. Basis 审核通过 Acquire
- merchant.t_merchant_creation_order Status: `ENABLED`
- merchant.t_merchant Status: `MERCHANT_ENABLED`
- member.tm_member / tm_member_identity 状态 1 激活
- member.tr_member_account 基本账户 `BASIC`
- member.tr_beneficiary_info 受益人卡信息
- ppcenter.t_product_apply_order / t_merchant_product_order（Merchant VAM Topup）
- dpm.t_dpm_outer_account_subset 外部账户分户
- statementii.t_settlement_config 对账单配置
- contract.t_contract 商户协议

### 3. Unified Portal 申请开通 WPS
- 接口：`api/acquiring/secure/merchant2/bizOpen/wps`
- 请求数据体：`bizAdminList`、`wpsInfoList`
- 写入：merchant.t_common_audit_order 商户公共审核

### 4. Basis 审核通过 WPS
- merchant.t_common_audit_order `audit_result:PASS`
- merchant.t_merchant_biz_open `["Acquire","WPS"]`
- merchant.t_biz_admin_info `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
- merchant.t_merchant_wps_info WPS 业务信息
- merchant.t_staff、merchant.t_staff_role
- member.tr_member_account `WPS_SALARY`
- vis.t_virtual_account `Status:Initial`

## QA 关注点
- 注册来源差异：Unified Portal / Agent / Basis / Botim 是否走相同落库链路
- 申请阶段会员状态须为 0(未激活)，审核通过后须翻为 1(激活)
- merchant.t_merchant_creation_order 应由申请态推进至 `ENABLED`，merchant.t_merchant 推进至 `MERCHANT_ENABLED`
- merchant.t_merchant_address 必须包含 `register` 与 `business` 两类地址
- merchant.t_merchant_biz_open 与 t_biz_admin_info 的角色枚举(`SUPPER_ADMIN`/`ACQUIRE_ADMIN`/`WPS_ADMIN`)与开通业务枚举(`Acquire`/`WPS`)一致性
- Acquire 审核通过后跨库副作用：ppcenter(Merchant VAM Topup)、dpm 分户、statementii 对账配置、contract 协议、member 基本账户(BASIC) 与受益人卡均应生成
- WPS 审核通过后 member.tr_member_account 须新增 `WPS_SALARY`，vis.t_virtual_account 初始为 `Initial`
- merchant.t_common_audit_order 仅在 `audit_result:PASS` 时推动 WPS 后续落库
- UAT 环境 Iban 手动推进，自动化用例需考虑该人工步骤
