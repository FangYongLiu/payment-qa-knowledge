---
title: 提现页面与选卡页面交互规则
domain: withdraw-to-bank
kind: wiki_page
slug: withdraw-to-bank-page-rules
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:bc1e3b1d-5f33-4288-87a2-3ca7a3a28ca7
tags: []
---

# 提现页面与选卡页面交互规则

本页描述 Transfer to Bank Account 功能在提现录入页与 Select Bank Account 选卡页的字段校验、KYC/VIP 差异，以及绑卡相关交互逻辑。功能整体说明见 [[withdraw-to-bank-overview]]。

## 功能入口

- wallet → withdraw → Transfer to Bank Account
- home → Transfer → Transfer to Bank Account
- 入口同时支持 iOS 与 Android

## 用户身份与提现页表现差异

- NoKYC：进入转账时自动跳转至实名认证页面
- KYC：Account holder name 默认填写实名认证的 name，且不可编辑
- VIP：Account holder name 默认为空，可编辑

## 提现页字段校验规则

### Account name
- KYC 不可编辑，VIP 可编辑
- 最大输入 30 个字符；输入后展示删除按钮
- 输入空格等同于空值；无值时显示文案：`Please enter holder name`
- 内容超出文本框时：
  - iOS：通过移动编辑指针查看
  - Android：支持点击拖动文本框左右移动查看

### IBAN
- 仅能输入英文和数字，最大 32 位；输入后展示删除按钮
- 无内容时展示：`Please enter a valid IBAN number.`
- 前端规则校验：`AE + 21 位数字`
- 校验失败：红色文本提示 `Please enter a valid IBAN number.`
- 前端校验通过后，离开文本框时通过接口对 IBAN 做规则校验

### Bank name
- 不可编辑，由接口对 IBAN 校验后返回
- 成功：展示接口返回的 Bank name
- 失败：toast 提示 `Something went wrong. Please check and re-enter your IBAN number.`

### Amount（AED）
- 仅能输入数字和小数点，输入后展示删除按钮
- 最大 10 位字符，小数点后最多 2 位
- 输入金额大于 Balance，点击 next：
  - iOS：文本框下方展示 `The amount you entered exceeds your available balance.`
  - Android：文本变红，文本框下方展示 `The amount you entered exceeds your available balance.`
- 输入 `0`、`0.0`、`0.00` 等同空值；空值点击 next：
  - iOS：文本框下方红色文案 `Please enter a vaild amount.`
  - Android：toast 提示 `Please enter a vaild amount.`

### Balance
- 进入页面时获取当前 AED 余额

### Transfer All
- 将 Balance 的值录入到 Amount（AED）

### View Price Plan
- 点击进入帮助中心查看 Price Plan

> 限额、费率与结算周期参见 [[withdraw-to-bank-limits-and-fees]]。

## Select Bank Account 页面（选卡页）

### 入口
- wallet → cards → 绑定提现卡
- 提现页选择已绑卡入口

### 选卡后回填
- 点击已绑定卡，直接将卡信息录入到提现页
- 回填后 holder name、IBAN、Bank name 均不可编辑

### 列表交互
- 列表为空时展示 No Record 图标
- 左滑展示删除按钮：
  - 点击 Confirm 确认删除
  - 点击 Cancel 关闭窗口

### 自动绑卡逻辑
- 提现成功时自动绑定该卡
- 将提交时的 holder name 保存为该提现卡的 `Bank_Account_Name`

## 收银台与风控

- 收银台展示：
  - Order Info：Transfer to Bank Account
  - 金额：Amount + Fee
  - Payment Method：仅能使用余额
- 风控：
  - 老版本未接风控：500 以上收银台出 OTP 验证，500 以内仅验证密码
  - 新版本接入风控核身后，由风控给出具体验证项

## 相关页面

- 提交后的状态、通知与账单展示见 [[withdraw-to-bank-bill-and-notification]]
- 测试方式见 [[withdraw-to-bank-test-guide]]
- 核心业务流程见 [[scn_withdraw_to_bank_main_flows]]
