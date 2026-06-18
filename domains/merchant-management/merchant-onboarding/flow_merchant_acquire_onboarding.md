---
id: flow_merchant_acquire_onboarding
object_type: Flow
domain: merchant-management
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:34ef57ae-73fe-4cd4-a064-e8edfb238167
tags:
- acquire
- onboarding
- merchant
subdomain: merchant-onboarding
module: null
sensitivity: normal
name: 商户Acquire开通端到端流程
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
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
描述商户通过 Unified Portal 提交 Acquire 业务申请，经 Basis 审核通过后激活 Acquire 业务的端到端流程。商户注册来源包括 Unified Portal、Agent、Basis、Botim。

## 步骤(跨系统)
1. **Unified Portal 提交申请 Acquire**
   - 调用申请商户接口：`/api/acquiring/permitAll/merchant/apply/add`
   - 开通业务可选：Acquire 或 WPS
   - 请求数据体：`acquireInfoList`、`addressList`、`bindingCard`、`bizAdminList`、`merchantData`、`partnerList`、`signatory`、`wpsInfoList`
   - 数据落库：
     - Merchant 商户库：`t_merchant_creation_order`(商户创建信息)、`t_merchant`(商户信息)、`t_merchant_address`(地址列表，类型 `["register","business"]`)、`t_partner`(合作伙伴信息)、`t_binding_card_apply_info`(绑卡信息)、`t_merchant_biz_open`(商户开通业务，`["Acquire","WPS"]`)、`t_biz_admin_info`(业务管理员，`["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`)、`t_merchant_acquire_info`(商户 Acquire 业务)、`t_staff`、`t_staff_role`
     - Member 会员库：`tm_member`(状态 0 未激活)、`tm_member_identity`(状态 0 未激活)

2. **Basis 审核通过 Acquire**
   - 数据更新：
     - Merchant 商户库：`t_merchant_creation_order` Status: `ENABLED`；`t_merchant` Status: `MERCHANT_ENABLED`
     - Member 会员库：`tm_member` 状态 1 激活；`tm_member_identity` 状态 1 激活；`tr_member_account` 基本账户 `BASIC`；`tr_beneficiary_info` 受益人卡信息
     - ppcenter 产品中心库：`t_product_apply_order`(Merchant VAM Topup)、`t_merchant_product_order`(Merchant VAM Topup)
     - dpm 会员账户库：`t_dpm_outer_account_subset` 外部账户分户表
     - statementii：`t_settlement_config` 对账单配置
     - contract：`t_contract` 商户协议

## 涉及服务/表
- **Merchant 商户库**：`t_merchant_creation_order`、`t_merchant`、`t_merchant_address`、`t_partner`、`t_binding_card_apply_info`、`t_merchant_biz_open`、`t_biz_admin_info`、`t_merchant_acquire_info`、`t_staff`、`t_staff_role`
- **Member 会员库**：`tm_member`、`tm_member_identity`、`tr_member_account`(BASIC)、`tr_beneficiary_info`
- **ppcenter 产品中心库**：`t_product_apply_order`、`t_merchant_product_order`
- **dpm 会员账户库**：`t_dpm_outer_account_subset`
- **statementii**：`t_settlement_config`
- **contract**：`t_contract`
- 关联接口：[[api_merchant_apply_add]]

## 校验点
- 申请阶段 `tm_member` / `tm_member_identity` 状态应为 0(未激活)
- 审核通过后 `t_merchant_creation_order.Status` = `ENABLED`，`t_merchant.Status` = `MERCHANT_ENABLED`
- 审核通过后 `tm_member` / `tm_member_identity` 状态应为 1(激活)
- `t_merchant_address` 地址类型须包含 `["register","business"]`
- `t_merchant_biz_open` 业务类型应包含 `Acquire`
- `t_biz_admin_info` 角色枚举：`["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
- `tr_member_account` 应创建 `BASIC` 基本账户
- ppcenter 产品订单应有 `Merchant VAM Topup` 类型
- 应生成对账单配置(`t_settlement_config`)和商户协议(`t_contract`)
