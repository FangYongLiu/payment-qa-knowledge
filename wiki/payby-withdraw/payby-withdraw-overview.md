---
title: PayBy提现到银行卡功能总览
domain: payby-withdraw
kind: wiki_page
slug: payby-withdraw-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/124289192
tags: []
---

# PayBy 提现功能总览

PayBy 提现(Withdraw)入口提供两种资金出账路径,用户在 Withdraw 页面进行选择。本页概述提现整体入口及「Transfer to Bank Account」功能的业务定位、常用场景与功能入口,便于快速理解提现业务全貌。

## 提现入口页面

- 页面标题:**Withdraw**
- 顶部导航包含返回按钮,点击进入后展示两个并列选项
- 每项均带有图标与右侧箭头指示进入下一步

### 两种提现方式

1. **Transfer to Bank Account**(转账至银行账户)
   - 图标:蓝色卡片
   - 用途:将余额提现到绑定的银行账户
   - 选择后进入银行账户提现流程
2. **Withdraw Cash**(提取现金)
   - 图标:绿色钞票
   - 选择后进入现金提取流程

两条路径相互独立,分别对应不同的后续操作链路。

## Transfer to Bank Account 业务描述

- 功能名称:Transfer to Bank Account(旧称 Transfer to your Bank)
- 用途:用户将余额账户的资金转入银行卡账户
- 与一般交易区别:业务双方为用户与银行,资金走向**离开 PayBy 体系**

### 常用场景

1. 用户进入提现页面,输入信息,提交提现,用户收到通知和账单
2. 银行返回成功,用户收到通知,账单更新
3. 银行返回失败,用户收到通知,账单更新,原路退款,**无退款订单**
4. 银行成功后进行退票,用户**无通知**,账单状态更新

### 功能入口

- wallet → withdraw → Transfer to Bank Account
- home → Transfer → Transfer to Bank Account
- 入口同时支持 iOS 与 Android

### 功能模块构成

- 提现表单页:录入 Account name / IBAN / Bank name / Amount,详见 [[payby-withdraw-page-rules]]
- History 页面与结果页轮询:每 10 秒轮询一次,成功/失败状态不再轮询;安卓 History 已改为对接 H5 账单
- Select Bank Account 页面:查看与选择已绑定提现卡,提现成功时自动绑定该卡(保存 holder name 为 Bank_Account_Name)
- 收银台:Order Info 显示 Transfer to Bank Account;金额为 Amount + Fee;Payment Method 仅支持余额
- 账单与通知:见 [[payby-withdraw-bill-notification]]
- 限额、费率、风控、结算:见 [[payby-withdraw-limits-fees]]

### 用户身份差异

- NoKYC:进入转账自动跳转实名认证页面
- KYC:Account holder name 默认填实名 name,不可编辑
- VIP:Account holder name 默认为空,可编辑

## 关联页面

- 端到端流程:[[flow_payby_withdraw_to_bank]]
- 核心测试场景:[[scn_payby_withdraw_core_cases]]
- 测试方法与版本迭代:[[payby-withdraw-test-and-versions]]

## 相关文档

- 产品原型:https://rv2lyl.axshare.com/#id=mxech9&p=%E6%9B%B4%E6%96%B0%E8%AE%B0%E5%BD%95&g=1
- 设计图:转账到银行卡-标注切图-0511.zip
