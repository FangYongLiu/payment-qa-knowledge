---
title: 提现页面与字段规则
domain: withdraw-cash
kind: wiki_page
slug: payby-withdraw-page-rules
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/124289192
tags: []
---

# 提现页面与字段规则

本页梳理 PayBy 提现到银行卡相关三个页面（提现页、History 页、Select Bank Account 页）的字段输入约束、交互规则与状态展示逻辑。功能整体定位与端到端流程见 [[payby-withdraw-overview]] 与 [[flow_payby_withdraw_to_bank]]。

## 功能入口

- wallet → withdraw → Transfer to Bank Account
- home → Transfer → Transfer to Bank Account

## 提现页面：用户身份与默认值

- NoKYC 用户：进入转账自动跳转实名认证页面
- KYC 用户：Account holder name 默认填充实名认证 name，**不可编辑**
- VIP 用户：Account holder name 默认为空，**可编辑**

## 提现页面：字段规则

### Account name
- KYC 不可编辑，VIP 可编辑
- 最大输入 30 个字符；输入内容后展示删除按钮
- 空格等同于空值；为空时展示文案：`Please enter holder name`
- 内容超出文本框时：
  - iOS：移动编辑指针来查看
  - Android：点击拖动文本框左右移动查看

### IBAN
- 仅允许英文和数字
- 最大输入 32 位；输入内容后展示删除按钮
- 为空时展示文案：`Please enter a valid IBAN number.`
- 前端规则校验：`AE + 21位数字`，校验失败给红色文本提示：`Please enter a valid IBAN number.`
- 前端校验通过后，离开文本框时调用接口对 IBAN 进行二次校验

### Bank name
- 不可编辑
- 通过接口对 IBAN 校验：
  - 成功：展示接口返回的 Bank name
  - 失败：toast 提示 `Something went wrong. Please check and re-enter your IBAN number.`

### Amount（AED）
- 仅允许数字和小数点；输入后展示删除按钮
- 最大 10 位字符，小数点后最多保留 2 位
- 输入金额大于下方 Balance，点击 next：
  - iOS：文本框下方展示文案 `The amount you entered exceeds your available balance.`
  - Android：文本变红 + 同样下方文案
- 输入 `0`、`0.0`、`0.00` 等同于空值，空值时点击 next：
  - iOS：文本框下方红色文案 `Please enter a vaild amount.`
  - Android：toast 提示 `Please enter a vaild amount.`

### Balance / Transfer All / View Price Plan
- Balance：进入页面时获取当前 AED 余额
- Transfer All：把 Balance 录入到 Amount（AED）
- View Price Plan：点击进入帮助中心的 Price Plan

## History 页面与结果轮询

> 注：Android History 已改为对接 H5 账单，本节描述为旧版/iOS 形态。

- 按月份分组，点击月份可选择时间，检索区间为 `[最早一笔订单时间, 选择时间]`
- 列表为空时展示 No Record 图标
- 结果页每 10 秒定时轮询一次；**成功 / 失败终态不再轮询**
- 结果页状态：提现提交 → 已提交至银行渠道 → 成功 / 失败

## Select Bank Account 页面

- 入口：wallet → cards → 绑定提现卡
- 列表为空时展示 No Record 图标
- 左滑显示删除按钮：
  - 点击 Confirm 确认删除
  - 点击 Cancel 关闭窗口
- 点击已绑定卡：直接将卡信息回填到提现页面，且 holder name、IBAN、Bank name 均**不可编辑**
- 提现成功时会自动绑定该卡；提交时的 holder name 会保存为该提现卡的 `Bank_Account_Name`

## 收银台展示

- Order Info：`Transfer to Bank Account`
- 金额：`Amount + Fee`
- Payment Method：**仅能使用余额**

---

相关：账单与通知文案见 [[payby-withdraw-bill-notification]]；限额、费率、风控规则见 [[payby-withdraw-limits-fees]]；测试用例与构造方式见 [[scn_payby_withdraw_core_cases]] 与 [[payby-withdraw-test-and-versions]]。
