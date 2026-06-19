---
title: VAM IBAN 充值方式UI说明
domain: vam-iban
kind: wiki_page
slug: vam-iban-recharge-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:38294281-d585-4350-913c-a62a58499e79
tags: []
---

# VAM IBAN 充值方式UI说明

本页记录 VAM IBAN 场景下 Recharge 页面的充值方式入口与 UI 展示。

## 页面概览

- 页面标题：**Recharge**（顶部居中，左上为返回箭头 `<`）
- 区块标签：**Recharge Via**
- 形态：三张垂直堆叠的可选卡片，分别对应一种充值方式

## 充值方式

页面提供以下三种 Recharge Via 选项：

1. **Debit Card**（绿色渐变卡片）
   - 描述：Support VISA or Mastercard debit card
   - 配图：手持一张黑色卡片

2. **uPay Kiosks**（蓝色渐变卡片）
   - 描述：Support 850+ uPay Kiosks in UAE
   - 配图：两台 uPay Kiosk 自助终端

3. **Bank Account Transfer**（珊瑚红/橙红渐变卡片，带红色边框高亮，为 VAM IBAN 场景的重点入口）
   - 描述：Use bank account to transfer to VAN account
   - 配图：手机示意图，展示 **PayBy Virtual Bank Account** 页面，含：
     - 账号 `1410 0444 2378 918`
     - `Capture Source` 按钮
     - `RECEIVE` 列表：`Sales`、`Transactions`、`International Transfer`
     - 部分可见的 `BENEFICIAL` 区块

## 交互说明

- 用户在三种方式中选择其一，对其 VAN（Virtual Account Number）账户进行充值。
- **Bank Account Transfer** 在 UI 上以红色边框高亮，作为 VAM IBAN 文档语境下被强调的入口。
