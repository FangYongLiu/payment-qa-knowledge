---
title: MG渠道汇款流程说明
domain: fund-out-transfer
kind: wiki_page
slug: mg-channel-overview
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d177e24c-5002-447d-b703-fbb9100fd016
tags: []
---

# MG渠道汇款流程说明

本页说明 MG 渠道跨境汇款确认页（Confirmation Page）的 UI 结构与各字段含义，用于 fund-out-transfer 业务域下的前端展示与字段核对。

## 页面整体结构

确认页自上而下包含以下区块：

1. Exchange Rate（汇率展示）
2. 付款方 / 收款方 金额对照
3. Beneficiary（收款人信息卡）
4. Payment Details（付款明细）
5. Receiving Currency（到账币种与预估金额）
6. Receiver's Transfer Details（收款人侧费用）

## Exchange Rate（汇率）

- 顶部展示参考汇率，例如：`1 AED ≈ 39.3812 JPY`
- 用于在用户提交前给出大致的换算预期。

## 付款方 / 收款方金额

左右分栏对照展示：

- 左侧：付款国家与币种
  - 国家：`United Arab Emirates`（含国旗图标）
  - 币种：`AED`
- 右侧：`You send` / 付款金额（示例：`1,000.00`）
- 左侧：收款国家与币种
  - 国家：`India`
  - 币种：`JPY`（注：示例截图中国家与币种存在不一致情况）
- 右侧：`Recipient receives` / 到账金额（示例：`39,379.41`）

## Beneficiary（收款人信息）

以卡片形式展示：

- 类型标签：`BANK TRANSFER`（蓝色 Tag）
- `Name`：收款人姓名（示例 `Kristin Watson`）
- `Phone`：收款人电话（示例 `+91 9717293980`）
- `Account`：收款账号（示例 `12875876324`）
- 右侧 Chip：到账币种 + 国旗图标（示例 `INR` + India 旗）

## Payment Details（付款明细）

以 label : value 形式列出，金额币种为付款币种 `AED`：

| 字段 | 示例 |
| --- | --- |
| Transfer Amount | AED 1,000.00 |
| Service Charge | AED 1.00 |
| VAT (5%) | AED 2.00 |
| **Amount Payable** | **AED 1,015.75** |

- `Amount Payable` 加粗显示，为用户实际需支付总额。

## Receiving Currency（到账币种）

- Disclaimer 文案：
  > Not all currencies available at all locations. The shown exchange rate is only an approximation. The actual exchange rate will be the rate that is in effect at the time the transfer is received.
- `Estimated Exchange Rate`：预估汇率（示例 `1 AED ≈ 39.2812 JPY`）
- `Estimated Receive Amount`：预估到账金额（示例 `JYP 39,379.41`，截图中币种缩写存在 `JYP` / `JPY` 拼写不一致）

## Receiver's Transfer Details（收款人侧费用）

- 提示文案：
  > Your beneficiary will be charged the following fees once they receive the amount.
- `Receiver's Fee`：收款人需承担的费用（示例 `-JYP 100.00`，以负号表示从到账金额中扣除）
- `Tax Collection`：收款人侧税费项

## 已知文案/数据不一致点

确认页示例中存在以下需注意的展示问题：

- 收款国家显示为 `India`，但币种显示为 `JPY`，国家与币种不匹配。
- Beneficiary 卡片右侧 Chip 显示为 `INR`，与上方 `JPY` 不一致。
- `Estimated Receive Amount` 中币种缩写写作 `JYP`，应为 `JPY`。

以上点在 QA 校验确认页字段渲染时需重点关注币种一致性与拼写。
