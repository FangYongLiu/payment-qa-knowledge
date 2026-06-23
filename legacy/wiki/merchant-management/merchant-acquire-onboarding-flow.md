---
title: 商户Acquire业务开通流程
domain: merchant-management
kind: wiki_page
slug: merchant-acquire-onboarding-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:34ef57ae-73fe-4cd4-a064-e8edfb238167
tags: []
---

# 商户Acquire业务开通流程

本页描述商户在 Unified Portal 提交 Acquire 业务申请、到 Basis 审核通过的完整链路，以及各阶段涉及的数据库表与状态变更。该流程属于 [[domain_merchant_management]]，端到端编排见 [[flow_merchant_acquire_onboarding]]，注册来源对比见 [[merchant-registration-sources]]。

## 流程概览

1. 商户在 Unified Portal 提交 Acquire 申请。
2. 系统在 Merchant、Member 库写入初始数据，会员处于未激活状态。
3. Basis 审核通过后，激活会员、生成基础账户与受益人信息，并初始化产品订单、对账单配置与合同。

## Step 1：Unified Portal 提交 Acquire 申请

- 接口：`/api/acquiring/permitAll/merchant/apply/add`，详见 [[api_merchant_apply_add]]
- 可开通业务：`Acquire` 或 `WPS`
- 请求数据体字段：
  - `acquireInfoList`
  - `addressList`
  - `bindingCard`
  - `bizAdminList`
  - `merchantData`
  - `partnerList`
  - `signatory`
  - `wpsInfoList`

### 涉及数据库

Merchant 商户库：

- `merchant.t_merchant_creation_order`：商户创建信息
- `merchant.t_merchant`：商户信息
- `merchant.t_merchant_address`：地址列表，类型 `["register","business"]`
- `merchant.t_partner`：合作伙伴信息
- `merchant.t_binding_card_apply_info`：绑卡信息
- `merchant.t_merchant_biz_open`：商户开通业务，取值 `["Acquire","WPS"]`
- `merchant.t_biz_admin_info`：商户业务管理员，角色 `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
- `merchant.t_merchant_acquire_info`：商户 Acquire 业务
- `merchant.t_staff`：商户员工信息
- `merchant.t_staff_role`：商户员工角色

Member 会员库（此时均为未激活）：

- `member.tm_member`：会员信息，状态 `0` 未激活
- `member.tm_member_identity`：会员标识，状态 `0` 未激活

## Step 2：Basis 审核通过 Acquire

审核通过后，商户与会员状态被激活，并联动产品中心、账户、对账单、合同等下游库。

### Merchant 商户库

- `merchant.t_merchant_creation_order`：`Status: ENABLED`
- `merchant.t_merchant`：`Status: MERCHANT_ENABLED`

### Member 会员库

- `member.tm_member`：状态 `1` 激活
- `member.tm_member_identity`：状态 `1` 激活
- `member.tr_member_account`：基本账户，类型 `BASIC`
- `member.tr_beneficiary_info`：受益人卡信息

### ppcenter 产品中心库

- `ppcenter.t_product_apply_order`：产品申请（`Merchant VAM Topup`）
- `ppcenter.t_merchant_product_order`：商户产品订单（`Merchant VAM Topup`）

### 其他

- `dpm.t_dpm_outer_account_subset`：外部账户分户表
- `statementii.t_settlement_config`：对账单配置
- `contract.t_contract`：商户协议

## 相关流程

- 同一申请入口若选择 WPS 业务，或后续追加开通 WPS，参见 [[merchant-wps-onboarding-flow]]。
