---
id: flow_merchant_register_acquire
object_type: Flow
domain: merchant-management
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/462749700
tags:
- merchant-register
- acquire
subdomain: null
module: null
sensitivity: normal
name: 商户注册并开通Acquire流程
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
描述从 Unified Portal 提交商户申请并开通 Acquire 业务，到 Basis 审核通过后端到端的数据落库流程。商户注册来源包括 Unified Portal、Agent、Basis、Botim、统一控台。

## 步骤(跨系统)
1. **Unified Portal 提交申请 Acquire**
   - 调用申请商户接口：`/api/acquiring/permitAll/merchant/apply/add`
   - 开通业务可选：Acquire 或 WPS
   - 请求数据体字段：`acquireInfoList`、`addressList`、`bindingCard`、`bizAdminList`、`merchantData`、`partnerList`、`signatory`、`wpsInfoList`
   - 数据落库到 Merchant 商户库与 Member 会员库（会员状态为 0 未激活）

2. **Basis 审核通过 Acquire**
   - 商户创建订单与商户信息状态推进为 `ENABLED` / `MERCHANT_ENABLED`
   - 会员及会员标识状态推进为 1 激活
   - 创建会员基本账户 `BASIC`、受益人卡信息
   - 在 ppcenter 创建产品申请与商户产品订单（Merchant VAM Topup）
   - 在 dpm 创建外部账户分户、statementii 创建对账单配置、contract 创建商户协议

## 涉及服务/表
**Step1 - Unified Portal 提交申请**

Merchant 商户库：
- `merchant.t_merchant_creation_order` 商户创建信息
- `merchant.t_merchant` 商户信息
- `merchant.t_merchant_address` 地址列表 `["register","business"]`
- `merchant.t_partner` 合作伙伴信息
- `merchant.t_binding_card_apply_info` 绑卡信息
- `merchant.t_merchant_biz_open` 商户开通业务 `["Acquire","WPS"]`
- `merchant.t_biz_admin_info` 商户业务管理员 `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
- `merchant.t_merchant_acquire_info` 商户 Acquire 业务
- `merchant.t_staff` 商户员工信息
- `merchant.t_staff_role` 商户员工角色

Member 会员库：
- `member.tm_member` 会员信息（状态 0 未激活）
- `member.tm_member_identity` 会员标识（状态 0 未激活）

**Step2 - Basis 审核通过 Acquire**

Merchant 商户库：
- `merchant.t_merchant_creation_order` Status: `ENABLED`
- `merchant.t_merchant` Status: `MERCHANT_ENABLED`

Member 会员库：
- `member.tm_member` 状态 1 激活
- `member.tm_member_identity` 状态 1 激活
- `member.tr_member_account` 基本账户 `BASIC`
- `member.tr_beneficiary_info` 受益人卡信息

ppcenter 产品中心库：
- `ppcenter.t_product_apply_order` 产品申请（Merchant VAM Topup）
- `ppcenter.t_merchant_product_order` 商户产品订单（Merchant VAM Topup）

其他：
- `dpm.t_dpm_outer_account_subset` 外部账户分户表
- `statementii.t_settlement_config` 对账单配置
- `contract.t_contract` 商户协议

## 校验点
- 提交申请后：商户创建订单/商户信息已写入；会员与会员标识状态为 0（未激活）
- 审核通过后：
  - `t_merchant_creation_order.Status = ENABLED`
  - `t_merchant.Status = MERCHANT_ENABLED`
  - `tm_member` 与 `tm_member_identity` 状态为 1（激活）
  - `tr_member_account` 已建立 `BASIC` 基本账户
  - ppcenter 已生成 Merchant VAM Topup 的产品申请与商户产品订单
  - dpm 外部账户分户、statementii 对账单配置、contract 商户协议均已落库
