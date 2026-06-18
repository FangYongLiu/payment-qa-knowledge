---
title: 商户WPS业务开通流程
domain: merchant-management
kind: wiki_page
slug: merchant-wps-onboarding-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:34ef57ae-73fe-4cd4-a064-e8edfb238167
tags: []
---

# 商户WPS业务开通流程

本页描述商户在 Unified Portal 申请开通 WPS 业务，到 Basis 审核通过为止涉及的接口与数据库表变更。

## 适用范围

- 来源渠道：Unified Portal
- 业务类型：WPS（Wage Protection System）
- 前置条件：商户已通过 Acquire 开通流程，详见 [[merchant-acquire-onboarding-flow]]

## 申请开通 WPS

由 Unified Portal 发起开通 WPS 业务申请。

- 接口：`api/acquiring/secure/merchant2/bizOpen/wps`
- 请求数据体：
  - `bizAdminList`
  - `wpsInfoList`

详见 [[api_merchant_bizopen_wps]]。

### 涉及数据库变更

- `merchant.t_common_audit_order` 商户公共审核（创建审核单）

## Basis 审核通过 WPS

Basis 审核通过后，落库正式的 WPS 业务信息及相关账户。

### Merchant 商户库

- `merchant.t_common_audit_order` 商户公共审核 —— `audit_result:PASS`
- `merchant.t_merchant_biz_open` 商户开通业务 —— `["Acquire","WPS"]`
- `merchant.t_biz_admin_info` 商户业务管理员 —— `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
- `merchant.t_merchant_wps_info` 商户 WPS 业务信息
- `merchant.t_staff` 商户员工信息
- `merchant.t_staff_role` 商户员工角色

### Member 会员库

- `member.tr_member_account` 基本账户 —— `WPS_SALARY`

### Vis 库

- `vis.t_virtual_account` 虚拟账户 —— `Status:Initial`

## 环境注意事项

- UAT 环境：Iban 需手动推进。

## 相关链接

- 端到端流程图：[[flow_merchant_wps_onboarding]]
- 注册来源总览：[[merchant-registration-sources]]
- 所属业务域：[[domain_merchant_management]]
