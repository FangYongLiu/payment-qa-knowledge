---
title: 结算与提现
domain: merchant-portal
kind: wiki_page
slug: merchant-portal-settlement-and-withdraw
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:0e957eb2-a24a-4257-b773-ebccfac51613
tags: []
---

# 结算与提现

本页介绍 PayBy 商户控台中的结算（Settlement）配置与手动提现（Withdraw）操作，包括截止时间设置、保留金额、自动结算开关，以及由管理员/财务账号完成的授权流程。

## 结算设置入口

进入路径：[Settings] – [Settlement]

## 自动结算与 Cut-off 时间

在 Settlement setting 中可配置：

- **自动结算开关**：Turn on/off automatic settlement
- **Cut-off time**：自动结算会在 cut-off 时间之后将资金发往银行
- **Daily Reserve amount**：每日保留金额，用于退款等场景的余额留存（参见 [[merchant-portal-refund]]）
- 修改设置需 **输入密码** 后点击 [SUBMIT] 生效

## 手动提现（Manually Withdraw）

操作路径：[Home] – [Withdraw]

步骤：
1. 输入提现金额
2. 点击 [Next]
3. 输入密码并点击 [Confirm]

权限规则：
- 需由 **admin 账号 / financial 账号** 授权
- 若由 financial staff 发起，则需由 admin 或另一个 financial 账号进行授权

## 手动提现授权流程

由具备授权权限的账号（admin / financial）执行：

[Settings] – [Authorizations] – [My Authorization] – [Authorize]

完成授权后，提现请求方可继续执行后台结算流程。

## 相关页面

- 添加/变更结算银行账户：[[merchant-portal-account-management]]
- 资金自动归集到商户账户：[[merchant-portal-virtual-bank-account]]
- 结算后对账与流水下载：[[merchant-portal-statements]]
- 退款相关授权：[[merchant-portal-refund]]
