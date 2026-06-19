---
title: 提现限额、费率与结算周期
domain: withdraw-cash
kind: wiki_page
slug: withdraw-to-bank-limits-and-fees
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:bc1e3b1d-5f33-4288-87a2-3ca7a3a28ca7
tags: []
---

# 提现限额、费率与结算周期

本页梳理 Transfer to Bank Account 功能在 KYC/VIP 用户下的限额限次、风控验证策略、费率历史变更，以及结算周期。功能整体说明见 [[withdraw-to-bank-overview]]，页面交互见 [[withdraw-to-bank-page-rules]]。

## 限额限次

按用户身份区分：

- **KYC**
  - 单日支出 10K AED
  - 单次支出 10K AED
- **VIP**
  - 无限制

## 风控与验证策略

收银台支付方式仅能使用余额。验证规则随版本演进：

- **老版本（未接风控）**
  - 金额 > 500：收银台出 OTP 验证
  - 金额 ≤ 500：仅需验证密码
- **新版本（接入风控核身后）**
  - 由风控给出具体验证项

收银台 Order Info 展示为 `Transfer to Bank Account`，金额为 `Amount + Fee`。

## 费率历史变更

- **2020/06/02**
  - 金额 > 50 AED：每笔收取 **2 AED** 费用
  - 金额 ≤ 50 AED：不收费
- **2020/10/09**
  - 金额 > 10 AED：每笔收取 **2 AED** 费用
  - 金额 ≤ 10 AED：不收费

提现页面提供 `View Price Plan` 入口，点击进入帮助中心查看费率说明。

## 结算周期

- **2020/06/02** 起：**T+1** 结算周期。

## 关联内容

- 账单与通知状态映射见 [[withdraw-to-bank-bill-and-notification]]
- 提现下单与结算的测试操作见 [[withdraw-to-bank-test-guide]]
- 端到端主流程参考 [[scn_withdraw_to_bank_main_flows]]
