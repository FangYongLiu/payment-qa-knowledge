---
title: PayBy提现交易详情页说明
domain: authorization-protocol
kind: wiki_page
slug: payby-withdrawal-transaction-detail
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a80371a5-f998-4607-b453-22d536798bd7
tags: []
---

# PayBy提现交易详情页说明

本页说明 PayBy App「提现到银行卡」交易详情页（Transaction Detail）的展示字段与示例数据。

## 页面概览

- 页面标题：Transaction Detail
- 业务标题：Transfer to Your Bank
- 顶部展示金额（负数表示出账）与交易状态
- 底部提供上一条 / 下一条交易切换（`<` / `>`）

## 头部展示字段

- **业务名称**：Transfer to Your Bank
- **金额**：`AED -3.00`（出账显示为负数）
- **状态**：Processing

## 交易明细字段

| 字段 | 示例值 | 说明 |
|---|---|---|
| Payment Method | Balance | 资金来源（余额） |
| Transfer Amount | AED 1.00 | 实际提现金额 |
| Fees | AED 2.00 | 手续费 |
| Transfer to | `************1010` First Abu Dhabi Bank PJSC | 目标银行卡（卡号脱敏）+ 银行名称 |
| Creation Time | 12-10-2020 13:21:55 | 交易创建时间 |
| Order No. | 131602480114014699 | 订单号 |

## 金额关系

- 顶部展示金额 = Transfer Amount + Fees
- 示例：`AED 3.00 = AED 1.00 + AED 2.00`
- 资金从 Balance 扣除，转入尾号 1010 的 First Abu Dhabi Bank PJSC 账户
- 当前状态为 Processing（处理中）
