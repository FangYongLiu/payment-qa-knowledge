---
title: Nublo外汇与卡交易结算方案
domain: ppc-card-business
kind: wiki_page
slug: nublo-fx-and-card-transaction-settlement
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:59c0c97d-afe6-440e-b5d9-9a6333b05ae3
tags: []
---

# Nublo外汇与卡交易结算方案

本页聚焦 Nublo 方案中的外汇 (FX) 与卡交易环节：对账文件字段、PayBy 的资金/利润记账动作，以及与 MasterCard 的结算处理。持卡人加载相关内容见 [[nublo-cardholder-loading-reconciliation]]，整体方案背景见 [[pcbs-ra-2406-nublo-deprecated-overview]]。

## 外汇 (Foreign Exchange)

### 系统序列
- Client 仅与 NymCard 集成，PayBy 不直接参与 FX 交互。

### FX 对账
- NymCard 向 Client 与 PayBy 提供 FX 对账文件。
- 对冲 (hedging tuning) 调整：
  - PayBy 向 NymCard 划款，或
  - NymCard 向 PayBy 划款。

### FX 对账文件字段
- FX Order ID
- Customer ID
- From Currency
- From Amount
- To Currency
- To Amount
- Profit Amount (AED)

### 资金划转规则
- AED → Foreign：将全额 AED 转给 NymCard。
- Foreign → AED：从 NymCard 收到全额 AED。
- **Profit Amount (AED)**：将该笔 AED 利润金额从 Escrow Account 划至 Profit Account。

## 卡交易 (Card Transaction)

### 交易处理
- Client 仅与 NymCard 集成。

### 交易结算流程
NymCard 向 Client 与 PayBy 提供交易对账文件，结算分为两部分：

**外币部分 (Foreign part)**
- NymCard 按结算币种 (settlement currency) 将金额转给 PayBy。
- PayBy 按比例将 AED 与 USD 金额转给 MasterCard。
- PayBy 将利润 (fees 与 interchange) 移入 client basic account。

### 交易对账文件字段
- Transaction ID
- Customer ID
- Wallet Currency
- Wallet Amount
- Customer Amount receive from NymCard (AED)
- Customer Amount to Settle (AED)
- Customer Amount to Profit (AED)
- Settlement Currency
- Settlement Amount
- Transaction Time
- Settlement Date
- Settlement Cycle

## 记账规则 (PayBy 侧)

### Customer Amount receive from NymCard (AED)
从 NymCard 收到的总额：
- DR: `0040`
- CR: `Client Customer Funds`

### Customer Amount to Settle (AED)
待与 MasterCard 结算的金额：
- DR: `Client Customer Funds`
- CR: `Settle Pending`

### Customer Amount to Profit (AED)
划为利润的金额：
- DR: `Client Customer Funds`
- CR: `Merchant Basic Account`

## 与 MasterCard 结算

- PayBy 按 AED / USD 拆分，将 `Customer Amount to Settle (AED)` 对应金额结算给 MasterCard。
- 具体结算实现：TODO（原文未细化）。

## 余额对账

- NymCard 向 Client 与 PayBy 提供卡余额数据。
- PayBy 进行 AED 余额的总额对账 (in total)。
