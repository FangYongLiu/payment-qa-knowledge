---
title: PayBy App 提现界面说明
domain: withdraw-cash
kind: wiki_page
slug: payby-app-withdraw-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:09736104-b43d-4951-bd69-4a416ba4ed34
tags: []
---

# PayBy App 提现界面说明

本页描述 PayBy App "Withdraw money"（提现）界面的 UI 元素布局、金额输入交互，以及两种提现方式（Aani / UAE bank）的费率与到账时效展示。

## 页面结构

提现界面自上而下包含以下元素：

- 顶部返回箭头（左上）
- 标题：**Withdraw money**
- 副标题：**Balance: 865.62 AED**（显示当前可用余额）
- 信息图标（i，右上）
- 金额输入框：以 Dirham 符号（₿/AED）开头，示例值 `500`
- 快捷金额选择 chip：
  - `500`（选中态，蓝色填充）
  - `Max`（未选中，白底）
- 链接：**View limit**（蓝色文本，跳转限额说明）
- 区块标题：**Choose your withdrawal method**
- 底部主按钮（蓝色 CTA）：**Proceed to Withdraw →**

## 金额输入与余额

- 用户在金额输入框中输入提现金额（示例 `500` AED）
- 提供 `500` 与 `Max` 两个快捷选项
- 当前余额：**865.62 AED**
- 选中 UAE bank 时，卡内附注：**Max withdraw amount: 863.62 AED**（即 余额 865.62 − 手续费 2.00）

## 提现方式选择

界面提供两种提现方式，每个方式以卡片形式展示，显示到账时效（⏱）与手续费（💰）。选中态以蓝色边框 + 右侧勾选标识表示。

### Aani（推荐）

- 标签：**Aani 👍 Recommended**
- 到账时效：**Instant**（即时到账）
- 手续费：**AED 0.50**
- 图标：深青色圆形图标
- 默认状态：未选中

### UAE bank

- 标签：**UAE bank**
- 到账时效：**1-2 days**
- 手续费：**AED 2.00**
- 图标：银行/建筑物图标
- 默认状态：选中
- 卡内附注：**Max withdraw amount: 863.62 AED**

## 操作流程

1. 用户输入或快捷选择提现金额
2. 选择提现方式（Aani 或 UAE bank）
3. 点击 **Proceed to Withdraw →** 进入下一步提现确认
