---
title: ToC 提现页面UI说明
domain: withdraw-cash
kind: wiki_page
slug: toc-withdraw-ui-screen
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a678aef6-cf86-4db1-a51c-ae1166720225
tags: []
---

# ToC 提现页面UI说明

PayBy App 用户端「Withdraw money」页面用于用户从余额发起提现，包含金额输入、提现方式选择与费率/到账时长展示。

## 页面布局

- 顶部返回箭头（左上）
- 标题：`Withdraw money`
- 副标题：`Balance: 865.62 AED`（展示当前可用余额）
- 信息 (i) 图标（右上）
- 金额输入区
- 提现方式选择区
- 底部主操作按钮：`Proceed to Withdraw →`（蓝色 CTA）

## 金额输入区

- 输入框前缀显示 AED 货币符号（₿ / Dirham symbol），示例值 `500`
- 快捷金额 chip 按钮：
  - `500`（选中态，蓝色填充）
  - `Max`（未选中，白色）
- 链接：`View limit`（蓝色文字，跳转查看限额）

## 提现方式（Choose your withdrawal method）

提供两种方式，每张卡片展示方式名称、到账时效 (⏱) 与手续费 (💰)：

| 方式 | 到账时效 | 手续费 | 备注 |
|---|---|---|---|
| `Aani` | Instant | AED 0.50 | 标记 `👍 Recommended` |
| `UAE bank` | 1-2 days | AED 2.00 | 当前选中（蓝色边框 + 右侧勾选） |

选中 `UAE bank` 时，卡片内附加提示：

- `Max withdraw amount: 863.62 AED`（即余额 865.62 − 手续费 2.00）

## 交互逻辑

- 用户输入提现金额，或通过 chip 快速选择 `500` / `Max`
- 选择一种提现方式（方式选中后卡片高亮，并展示对应最大可提现金额）
- 点击 `Proceed to Withdraw →` 进入提现确认流程
