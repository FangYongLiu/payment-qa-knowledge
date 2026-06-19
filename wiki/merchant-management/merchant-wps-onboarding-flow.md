---
title: 商户WPS业务开通流程
domain: merchant-management
kind: wiki_page
slug: merchant-wps-onboarding-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e0a7a237-82a3-4940-8229-3f398d64e5b0
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

## 员工侧 Salary Card 体验

WPS 业务开通且账户落库后，员工可在 Botim Money / PayBy App 中访问 Salary Card 页面（标题 "Salary Card"），用于自助管理薪资卡。

- 卡片形态：虚拟 Mastercard 借记卡，正面包含：
  - 左上：`Botim Money` 标识
  - 右上：`PayBy` 标识及 NFC 非接触支付标志
  - 中部：嵌入 "b" Logo 的二维码
  - 卡号显示为掩码（如 `•••• •••• •••• 7466`），可通过眼睛图标切换显示
  - 右下：Mastercard 标识
  - 提示：`Tap card to view details`
- Card Management 自助功能列表：
  1. Transactions —— 查看交易明细
  2. Lock Card —— 锁卡
  3. Reset ATM PIN —— 重置 ATM 密码
  4. Replace Card —— 换卡
  5. Fees & Charges —— 查看费用
- 页脚：`Powered by PayBy`

## 相关链接

- 端到端流程图：[[flow_merchant_wps_onboarding]]
- 注册来源总览：[[merchant-registration-sources]]
- 所属业务域：[[domain_merchant_management]]
