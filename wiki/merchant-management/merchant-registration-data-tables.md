---
title: 商户注册与开通涉及的数据库表
domain: merchant-management
kind: wiki_page
slug: merchant-registration-data-tables
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/462749700
tags: []
---

# 商户注册与开通涉及的数据库表

本页梳理商户从注册申请，到 Acquire 业务开通、WPS 业务开通各阶段涉及的数据库、表以及关键字段的状态变化。相关流程见 [[flow_merchant_register_acquire]] 与 [[flow_merchant_open_wps]]，整体上下文见 [[merchant-management-overview]]。

## 商户注册来源

商户注册申请可来自以下渠道：

- Unified Portal
- Agent
- Basis
- Botim
- 统一控台

## 阶段一：Unified Portal 提交申请 Acquire

调用接口 [[api_merchant_apply_add]]：`/api/acquiring/permitAll/merchant/apply/add`，可同时申请开通 `Acquire` 或 `WPS`。

请求数据体包含：`acquireInfoList`、`addressList`、`bindingCard`、`bizAdminList`、`merchantData`、`partnerList`、`signatory`、`wpsInfoList`。

### 涉及数据库表

**Merchant 商户库**

- `merchant.t_merchant_creation_order` — 商户创建信息
- `merchant.t_merchant` — 商户信息
- `merchant.t_merchant_address` — 地址列表，类型 `["register","business"]`
- `merchant.t_partner` — 合作伙伴信息
- `merchant.t_binding_card_apply_info` — 绑卡信息
- `merchant.t_merchant_biz_open` — 商户开通业务，`["Acquire","WPS"]`
- `merchant.t_biz_admin_info` — 商户业务管理员，`["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
- `merchant.t_merchant_acquire_info` — 商户 Acquire 业务
- `merchant.t_staff` — 商户员工信息
- `merchant.t_staff_role` — 商户员工角色

**Member 会员库**

- `member.tm_member` — 会员信息，状态 `0` 未激活
- `member.tm_member_identity` — 会员标识，状态 `0` 未激活

## 阶段二：Basis 审核通过 Acquire

审核通过后，商户主体激活，并联动产品、账户、对账与合同等下游库。

### 涉及数据库表

**Merchant 商户库**

- `merchant.t_merchant_creation_order` — Status: `ENABLED`
- `merchant.t_merchant` — Status: `MERCHANT_ENABLED`

**Member 会员库**

- `member.tm_member` — 状态 `1` 激活
- `member.tm_member_identity` — 状态 `1` 激活
- `member.tr_member_account` — 基本账户 `BASIC`
- `member.tr_beneficiary_info` — 受益人卡信息

**ppcenter 产品中心库**

- `ppcenter.t_product_apply_order` — 产品申请（Merchant VAM Topup）
- `ppcenter.t_merchant_product_order` — 商户产品订单（Merchant VAM Topup）

**dpm 会员账户库**

- `dpm.t_dpm_outer_account_subset` — 外部账户分户表

**statementii 账单**

- `statementii.t_settlement_config` — 对账单配置

**contract 合同**

- `contract.t_contract` — 商户协议

## 阶段三：Unified Portal 申请开通 WPS

调用接口 [[api_merchant_bizopen_wps]]：`api/acquiring/secure/merchant2/bizOpen/wps`。

请求数据体包含：`bizAdminList`、`wpsInfoList`。

### 涉及数据库表

- `merchant.t_common_audit_order` — 商户公共审核

## 阶段四：Basis 审核通过 WPS

审核通过后写入 WPS 相关业务表与账户表。

### 涉及数据库表

**Merchant 商户库**

- `merchant.t_common_audit_order` — `audit_result:PASS`
- `merchant.t_merchant_biz_open` — `["Acquire","WPS"]`
- `merchant.t_biz_admin_info` — `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
- `merchant.t_merchant_wps_info` — 商户 WPS 业务信息
- `merchant.t_staff` — 商户员工信息
- `merchant.t_staff_role` — 商户员工角色

**Member 会员库**

- `member.tr_member_account` — 基本账户 `WPS_SALARY`

**Vis**

- `vis.t_virtual_account` — 虚拟账户，Status: `Initial`

## 环境补充说明

- UAT 环境下需手动推进 Iban。
