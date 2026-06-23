---
title: MG渠道转账汇总页面说明
domain: channel-integration
kind: wiki_page
slug: mg-channel-transfer-summary-ui
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:1ae4c51b-d6d2-4e49-85b5-1a102c47ee69
tags: []
---

# MG渠道转账汇总页面说明

本页记录 MG（MoneyGram）渠道在转账确认/汇总页面的 UI 字段构成、汇率展示规则，以及当前页面发现的若干 UI 与数值一致性问题。

## 页面字段构成

汇总页自上而下展示以下金额明细（以 AED → JPY 转账为例）：

- **Transfer Amount**：转账本金，例如 `AED 1,000.00`
- **Service Charge**：服务费，例如 `AED 1.00`
- **VAT (5%)**：增值税，例如 `AED 2.00`
- **Amount Payable**（加粗）：应付总额，例如 `AED 1,015.75`

## Receiving Currency 区块

页面下方以独立区块展示收款币种相关信息，包含免责声明与两个估算字段。

### 免责声明文案

- "Not all currencies available at all locations."
- "The shown exchange rate is only an approximation. The actual exchange rate will be the rate that is in effect at the time the transfer is received."

即：并非所有币种在所有网点均可收款；展示汇率仅为估算值，实际汇率以转账被领取时的即时汇率为准。

### 估算字段

- **Estimated Exchange Rate**：估算汇率，例如 `1 AED ≈ 39.2812 JPY`
- **Estimated Receive Amount**：估算收款金额，例如 `JYP 39,379.41`

## 已知 UI / 数据问题

以下问题在示例截图中被识别，需关注修复：

### 1. 币种代码拼写错误（JYP vs JPY）

- `Estimated Receive Amount` 行显示为 `JYP 39,379.41`，应为标准 ISO 代码 `JPY`。
- 同页 `Estimated Exchange Rate` 行的 `JPY` 拼写正确，存在前后不一致。

### 2. 金额合计不一致

明细行加和与 `Amount Payable` 不相等：

- `1,000.00 + 1.00 + 2.00 = 1,003.00`
- 但 `Amount Payable` 显示为 `1,015.75`

差额约 `12.75`，疑似存在未在页面展示的费用/税项行，或属于显示/取整缺陷。

### 3. Estimated Receive Amount 计算来源不明

以展示汇率 `39.2812` 验证：

- 用 Transfer Amount：`1,000 × 39.2812 = 39,281.20`
- 用 Amount Payable：`1,015.75 × 39.2812 ≈ 39,900`
- 实际显示：`39,379.41`

两种推算均无法精确匹配显示值，估算收款金额的计算口径需进一步确认。
