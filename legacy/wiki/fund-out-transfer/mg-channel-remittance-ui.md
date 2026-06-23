---
title: MG渠道汇款确认页说明
domain: fund-out-transfer
kind: wiki_page
slug: mg-channel-remittance-ui
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:59dbaa7a-0560-4280-a6ed-44cb402a4549
tags: []
---

# MG渠道汇款确认页说明

本页说明 MG（MoneyGram）渠道下汇款确认页的 UI 结构与字段含义，覆盖汇率、收发款方、手续费、税费等明细展示。

## 页面顶部：汇率展示

- 标题：**Exchange Rate**
- 展示参考汇率，例如：`1 AED ≈ 39.3812 JPY`

## 收发款方区块

左右对照展示发款方与收款方信息：

- 左侧（发款方）：
  - 国家：United Arab Emirates（含国旗图标）
  - 币种：AED
- 右侧（发款方金额）：
  - 标签：**You send**
  - 金额：`1,000.00`
- 左侧（收款方）：
  - 国家：India
  - 币种：JPY
- 右侧（收款方金额）：
  - 标签：**Recipient receives**
  - 金额：`39,379.41`

## 收款人卡片（Beneficiary）

- 类型标签：`BANK TRANSFER`
- Name：收款人姓名（示例：Kristin Watson）
- Phone：收款人电话（示例：+91 9717293980）
- Account：收款账号（示例：12875876324）
- 右侧 Chip：收款币种 + 国旗（示例：INR + 印度国旗）

## 付款明细（Payment Details）

以"标签 : 数值"形式展示：

- **Transfer Amount**：转账金额（示例：AED 1,000.00）
- **Service Charge**：服务费（示例：AED 1.00）
- **VAT (5%)**：增值税（示例：AED 2.00）
- **Amount Payable**：应付总额，加粗展示（示例：AED 1,015.75）

## 收款币种区块（Receiving Currency）

- 免责说明：`Not all currencies available at all locations. The shown exchange rate is only an approximation. The actual exchange rate will be the rate that is in effect at the time the transfer is received.`
- **Estimated Exchange Rate**：预估汇率（示例：`1 AED ≈ 39.2812 JPY`）
- **Estimated Receive Amount**：预估到账金额（示例：JYP 39,379.41）

## 收款方扣费明细（Receiver's Transfer Details）

- 说明文案：`Your beneficiary will be charged the following fees once they receive the amount.`（收款人到账时将被扣除以下费用）
- **Receiver's Fee**：收款方手续费（示例：-JYP 100.00）
- **Tax Collection**：税费扣缴
