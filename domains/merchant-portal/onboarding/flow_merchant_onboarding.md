---
id: flow_merchant_onboarding
object_type: Flow
domain: merchant-portal
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:fa5361b9-9768-4302-b8dc-f2dd9cc50451
tags:
- onboarding
- cross-system
- kyb
- aml
subdomain: onboarding
module: null
sensitivity: normal
name: 商户Onboarding端到端流程
aliases: []
related_services:
- svc_member
- svc_merchant
- svc_basis_merchant
- svc_aml
- svc_vis
- svc_billing
- svc_contract
- svc_unified_portal
related_tables:
- t_merchant_creation_order
- t_merchant
- t_merchant_address
- t_partner
- t_binding_card_apply_info
- t_merchant_biz_open
- t_biz_admin_info
- t_merchant_acquire_info
- t_staff
- t_staff_role
- tm_member
- tm_member_identity
- tr_member_account
- tr_beneficiary_info
- t_product_apply_order
- t_merchant_product_order
- t_dpm_outer_account_subset
- t_dpm_account_crl_def
- t_settlement_config
- t_contract
- t_virtual_account
related_scenarios:
- scn_acquire_product_apply
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
商户Onboarding是一个跨系统流程，从用户在Unified Portal注册/登录开始，到BMOC后台完成KYB审核结束。商户只有在Member、Merchant、Basis、AML、VIS、Billing、Contract等所有服务全部成功处理后，才能成为可用状态(usable)。AML失败会阻断商户激活。

## 步骤(跨系统)

### Step 1: Merchant Registration/Login (前端 Unified Portal)
- 入口：`https://sim-web-unified.test2pay.com/verify/login` (sim) / `https://uat-web-unified.test2pay.com/verify/login` (uat)
- 首次注册默认通过 OTP 登录，登录后必须设置密码
- sim 环境默认 OTP=161616；uat 环境需要 real OTP
- 测试账号：Mobile `+971-556579167`, Password `132580` 或 `Yong0324####`

### Step 2: Merchant Onboarding 表单填写
- 填写 Onboarding form 信息
- Company Bank Account 字段 IBAN（如 `AE790030013112189920001`）由后端服务校验

### Step 3: Merchant Business Type Choose
- Company Business Type 选择 `Payment`(即 Merchant Acquire Service) 或 WPS
- 填写 Administrator Information，Mobile number 即注册成功后用于登录控台的手机号，且具有 administrator role

### Step 4: BMOC 后台审核 (Merchant Status Approval)
- 登录 BMOC：`https://sim-admin.corp.test2pay.com/basis-cas/login?service=https://sim-admin.corp.test2pay.com/bmoc/cas`
- 菜单路径：`Basis Merchant => Business => Merchant => Merchant Onboarding`
- Step 1：complete AML Risk Calculate(AML 风险计算)
- Step 2：complete KYB Approval(KYB 审批)

### Step 5: 状态确认
- 系统处理完成后，在 BMOC 中检查 merchant status 是否为可用状态

## 涉及服务/表

### 服务(Service Definition & Responsibilities)
| 服务 | 职责 |
|---|---|
| Member | 中央用户身份服务，管理 member 账户，提供下游使用的 Member ID |
| Merchant | 商户域服务，管理 merchant profile、onboarding 状态、merchant–member 关系、生命周期 |
| Basis | 核心基础服务，处理账户启用、产品激活、运营审核决策、内部核心配置 |
| AML | 反洗钱服务，对商户和牌照信息进行合规与风险筛查；AML 失败将阻断商户激活 |
| VIS | Virtual IBAN 服务，创建和管理虚拟 IBAN 账户及外部对接 |
| Billing | 账单与会计服务，负责 billing account 创建、订单初始化、财务结算配置 |
| Contract | 合同管理服务，onboarding 成功后生成和管理商户合同 |
| Unified Portal | 商户注册和 onboarding 提交的前端入口 |

### 数据表(Merchant Onboarding impact database scope)
- **Merchant**：`t_merchant_creation_order`、`t_merchant`、`t_merchant_address`、`t_partner`、`t_binding_card_apply_info`、`t_merchant_biz_open`、`t_biz_admin_info`、`t_merchant_acquire_info`、`t_staff`、`t_staff_role`
- **Member**：`tm_member`、`tm_member_identity`、`tr_member_account`、`tr_beneficiary_info`
- **Ppcenter**：`t_product_apply_order`、`t_merchant_product_order`
- **Dpm**：`t_dpm_outer_account_subset`、`t_dpm_account_crl_def`
- **Statemenii**：`t_settlement_config`
- **Contract**：`t_contract`
- **Vis**：`t_virtual_account`(Iban Top up)

## 校验点
- 注册环节：sim 用默认 OTP `161616`；uat 必须使用 real OTP
- IBAN 字段由后端校验，需使用合法值(示例 `AE790030013112189920001`)
- BMOC 审核需依次完成 AML Risk Calculate 与 KYB Approval 两步
- AML 校验失败将阻断后续商户激活
- 商户必须在所有服务(Member/Merchant/Basis/AML/VIS/Billing/Contract)全部成功后才可用
- 通过查询 `t_merchant_creation_order`、`t_merchant`、`tm_member` 等表确认 onboarding 数据落库情况
- 选择 Business Type=Payment 后，进入收单商户控台流程(详见 [[scn_acquire_product_apply]])
