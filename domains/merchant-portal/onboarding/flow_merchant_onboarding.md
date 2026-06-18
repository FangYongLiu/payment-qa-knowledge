---
id: flow_merchant_onboarding
object_type: Flow
domain: merchant-portal
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/997785804
tags:
- onboarding
- cross-system
- KYB
- AML
subdomain: onboarding
module: null
sensitivity: normal
name: 商户入驻端到端流程
aliases: []
related_services:
- gp251_unified-merchant-portal
- gp044_merchant
- gp161_basis-merchant
- gp005_member
- gp209_aml
- gp149_vis
- gp107_contract
related_tables:
- t_merchant_creation_order
- t_merchant
- t_merchant_biz_open
- t_biz_admin_info
- t_merchant_acquire_info
- tm_member
- tm_member_identity
- tr_member_account
- t_contract
- t_virtual_account
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
商户入驻是一个跨系统流程：由 Unified Portal 作为前端入口提交注册与入驻表单，后续 Member、Merchant、Basis、AML、VIS、Billing、Contract 等服务协同处理；只有当所有服务全部成功后，商户才进入可用状态。BMOC 后台负责 AML Risk Calculate 与 KYB Approval 两步审核动作；AML 失败将阻断商户激活。

## 步骤(跨系统)
1. **注册/登录(Unified Portal)**
   - 入口：`https://sim-web-unified.test2pay.com/verify/login`(SIM) / `https://uat-web-unified.test2pay.com/verify/login`(UAT)
   - 首次注册默认通过 OTP 登录，登录后必须设置密码；SIM 默认 OTP 为 `161616`，UAT 需真实 OTP。
2. **填写 Onboarding 表单**
   - 录入公司信息、Company Bank Account(如 IBAN：`AE790030013112189920001`)；该 IBAN 字段由后端服务校验。
3. **选择商户业务类型**
   - Company Business Type 选择 `Payment`(即 Merchant Acquire Service) 或 WPS。
   - 录入 Administrator Information：管理员手机号将作为登录账号且持有 administrator 角色。
4. **提交后跨服务处理**
   - Member：建立/复用 Member ID 与身份、账户信息。
   - Merchant：创建商户档案、入驻状态、商户–会员关系。
   - Basis：账户启用、产品激活、运营审核决策与核心配置。
   - AML：对商户与执照信息进行合规与风险筛查；失败则阻断激活。
   - VIS：创建并管理 Virtual IBAN(用于 IBAN Top up)。
   - Billing：账单账户创建、订单初始化、结算配置。
   - Contract：商户成功入驻后生成并管理合同。
5. **BMOC 审核(Merchant Status Approval)**
   - 登录：`https://sim-admin.corp.test2pay.com/basis-cas/login?service=https://sim-admin.corp.test2pay.com/bmoc/cas`
   - 菜单路径：`Basis Merchant => Business => Merchant => Merchant Onboarding`
   - Step 1：complete AML Risk Calculate
   - Step 2：complete KYB Approval
6. **完成与状态确认**
   - 系统处理完毕后在 BMOC 检查商户状态；全部服务成功后商户进入可用状态。

## 涉及服务/表
**服务(及职责)**
- Unified Portal(`gp251_unified-merchant-portal`)：注册与入驻提交前端入口。
- Member(`gp005_member`)：跨系统统一身份，提供 Member ID。
- Merchant(`gp044_merchant`)：商户档案、入驻状态、商户–会员关系、生命周期。
- Basis(`gp161_basis-merchant`)：账户启用、产品激活、运营审核、核心配置。
- AML(`gp209_aml`)：合规与风险筛查，失败阻断激活。
- VIS(`gp149_vis`)：Virtual IBAN 创建与外部对接。
- Billing：账单账户、订单初始化、结算配置。
- Contract(`gp107_contract`)：合同生成与管理。

**数据库与表**
- Merchant：`t_merchant_creation_order`、`t_merchant`、`t_merchant_address`、`t_partner`、`t_binding_card_apply_info`、`t_merchant_biz_open`、`t_biz_admin_info`、`t_merchant_acquire_info`、`t_staff`、`t_staff_role`
- Member：`tm_member`、`tm_member_identity`、`tr_member_account`、`tr_beneficiary_info`
- Ppcenter：`t_product_apply_order`、`t_merchant_product_order`
- Dpm：`t_dpm_outer_account_subset`、`t_dpm_account_crl_def`
- Statemenii：`t_settlement_config`
- Contract：`t_contract`
- Vis：`t_virtual_account`(IBAN Top up)

## 校验点
- 登录方式：首次注册默认 OTP，登录后需设置密码；SIM OTP=`161616`，UAT 必须真实 OTP。
- IBAN 字段由后端校验(示例：`AE790030013112189920001`)。
- Business Type 选 `Payment` 走 Merchant Acquire Service 路径；管理员手机号决定登录账号与 administrator 角色。
- BMOC 审核必须依次完成 AML Risk Calculate 与 KYB Approval；AML 失败阻断商户激活。
- 入驻完成需检查商户状态；只有当 Member/Merchant/Basis/AML/VIS/Billing/Contract 全部成功，商户才可用。
- 数据库验证范围覆盖 Merchant / Member / Ppcenter / Dpm / Statemenii / Contract / Vis 上述表的写入与状态。
