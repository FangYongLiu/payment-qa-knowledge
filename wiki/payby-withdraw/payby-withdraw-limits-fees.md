---
title: 提现限额、费率、风控与结算
domain: payby-withdraw
kind: wiki_page
slug: payby-withdraw-limits-fees
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/124289192
tags: []
---

# 提现限额、费率、风控与结算

本页汇总 PayBy 提现到银行卡的限额限次、费率历史、风控验证逻辑与结算周期。其余功能与流程见 [[payby-withdraw-overview]]。

## 限额限次

按用户身份区分：

- **KYC**
  - 单日支出：10K AED
  - 单次支出：10K AED
- **VIP**
  - 无限制

KYC 与 VIP 在提现页面的字段编辑权限差异详见 [[payby-withdraw-page-rules]]。

## 费用及费率

按时间节点变更：

- **2020/06/02**
  - `>50 AED`：每笔收取 2 AED 费用
  - `<=50 AED`：不收费
- **2020/10/09**
  - `>10 AED`：每笔收取 2 AED 费用
  - `<=10 AED`：不收费

收银台展示口径：`Amount + Fee`，且 Payment Method 仅能使用余额。

## 结算周期

- **2020/06/02**：T+1 的结算周期

## 风控逻辑

收银台环节的核身验证由版本决定：

- **老版本（未接风控）**
  - 500 以上：收银台出 OTP 验证
  - 500 以内：仅需验证密码
- **新版本（已接风控核身）**
  - 由风控引擎给出具体验证项

## 相关链接

- 字段与页面校验规则：[[payby-withdraw-page-rules]]
- 账单/通知状态映射：[[payby-withdraw-bill-notification]]
- 端到端流程：[[flow_payby_withdraw_to_bank]]
- 核心测试场景：[[scn_payby_withdraw_core_cases]]
- 测试方法与版本迭代：[[payby-withdraw-test-and-versions]]
