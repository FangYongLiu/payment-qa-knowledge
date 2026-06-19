---
title: ToC Withdraw 交易历史页面UI说明
domain: withdraw-cash
kind: wiki_page
slug: toc-withdraw-transaction-history-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b12e2ce8-9084-4eda-b75c-c3b1fd308c15
tags: []
---

# ToC Withdraw 交易历史页面UI说明

本页基于 ToC Withdraw 业务域下的移动端 Transaction History 页面截图，说明该页的UI布局、元素构成与汇总数据的对账逻辑。

## 页面布局

页面整体为 iOS 端 Transaction History 页面，自上而下分为：状态栏、页面头部、筛选行、汇总卡片、交易列表。

## 页面头部

- 左侧：返回箭头（Back）
- 中间：标题 `Transaction History`
- 右侧：关闭按钮 `X`

## 筛选行

- 左侧：月份选择器，示例值 `Mar 2026`，带下拉箭头
- 右侧：筛选/设置图标（sliders glyph）

## 汇总卡片（Summary）

浅紫色（lavender）背景卡片，分为两列：

- **Incoming**（左列）：示例值 `+ AED 0.00`，绿色文字
- **Outgoing**（右列）：示例值 `- AED 2.01`

## 交易列表

列表项以浅紫色卡片样式展示，单条交易包含：

- 标题：`Transfer to Bank Account`
- 副标题/时间戳：`23 Mar 2026 · 03:01 PM`
- 金额（右对齐）：`AED -2.01`

示例截图中仅有一条交易记录，其余区域为空。

## 汇总与列表的对账逻辑

汇总卡片的金额与列表中的交易记录保持一致：

- 当月仅一笔出账（Transfer to Bank Account，金额 AED 2.01），对应 Outgoing 合计 `- AED 2.01`
- 当月无入账交易，Incoming 合计为 `+ AED 0.00`
- 即：Outgoing 总额 = 当月所有出账交易之和；Incoming 总额 = 当月所有入账交易之和

该页面对应 Withdraw 业务域中提现交易的历史查看入口。
