---
title: 账户与员工管理
domain: merchant-portal
kind: wiki_page
slug: merchant-portal-account-management
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:0e957eb2-a24a-4257-b773-ebccfac51613
tags: []
---

# 账户与员工管理

本页介绍 PayBy 商户控台中银行账户的添加/变更流程，以及员工账号(Add Staff)的创建与管理员授权步骤。员工创建、提现、退款等敏感操作均需管理员或财务账号授权后生效。

## 添加 / 变更银行账户

银行账户的添加或变更不在控台自助完成，需通过邮件申请：

- 联系邮箱：**merchant@payby.com**
- 需提供材料：
  1. 一份**加盖公司印章的官方信函**(Official Letter with Company Seal)，内容包含：
     - PayBy MID
     - Bank Account Holder Name (持有人名称需与营业执照上的公司名一致)
     - IBAN
     - Beneficiary Address
     - Bank Name
  2. **Bank Letter / Statement**：需显示 Account Name 和 IBAN

变更后的银行账户用途与提现/结算流程参见 [[merchant-portal-settlement-and-withdraw]]。

## 添加员工 (Add Staff)

入口路径：

- **[Management] → [Merchant Management] → [Staff Information] → [+ ADD STAFF]**

注意事项：

- 添加员工的操作 **需要管理员(admin)账号授权后生效**。

## Add Staff 授权流程

由管理员账号完成授权：

- 路径：**[Settings] → [Authorizations] → [My Authorization] → [Authorize]**
- 管理员在该页面找到对应的添加员工请求并执行 Authorize。

## 与授权机制相关的其他操作

控台中以下操作同样依赖管理员/财务账号的授权机制，授权入口与上述一致(均位于 [Settings] → [Authorizations])：

- 手动提现 (Manually Withdraw)：详见 [[merchant-portal-settlement-and-withdraw]]
- 退款 (Refund)：详见 [[merchant-portal-refund]]

如需了解登录方式与控台整体功能，参见 [[merchant-portal-sign-in]] 与 [[merchant-portal-overview]]。
