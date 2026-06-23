---
title: Nublo外汇与卡交易清算流程
domain: ppc-card-business
kind: wiki_page
slug: nublo-fx-and-transaction-settlement
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/564101170
tags: []
---

# Nublo外汇与卡交易清算流程

本页聚焦 Nublo 在外汇（FX）、卡交易及与 MasterCard 清算环节的对账文件、记账动作与利润账户处理逻辑。持卡人加载相关流程见 [[nublo-cardholder-loading-flow]]，整体资金流概览见 [[pcbs-ra-2406-nublo-deprecated]]。

## 外汇（FX）流程

### 系统对接
- Client 仅与 NymCard 集成，PayBy 不直接参与 FX 下单链路。

### FX 对账文件
NymCard 向 Client 与 PayBy 提供 FX 对账文件，字段包括：

- FX Order ID
- Customer ID
- From Currency
- From Amount
- To Currency
- To Amount
- Profit Amount (AED)

### 资金划拨（Hedging Tuning）
依据对账结果在 PayBy 与 NymCard 间双向划拨以做对冲调整：

- **AED → 外币**：PayBy 向 NymCard 转出对应的 AED 总额。
- **外币 → AED**：PayBy 从 NymCard 收取对应的 AED 总额。

### 利润处理
- `Profit Amount (AED)`：将该 AED 金额从 Escrow Account 划入 Profit Account。

## 卡交易流程

### 交易链路
- Client 仅与 NymCard 集成完成卡交易处理。

### 交易对账文件
NymCard 向 Client 与 PayBy 提供交易对账文件，字段包括：

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

### 清算执行步骤
依据对账文件，PayBy 执行以下动作：

1. NymCard 按 settlement currency 向 PayBy 划拨外币部分金额。
2. PayBy 将 AED 与 USD 部分按对应金额清算给 MasterCard。
3. PayBy 将利润（fees 与 interchange）划入 Client Basic Account。

## 记账规则（Wallet / Settlement / Profit）

| 字段 | 含义 | 借（DR） | 贷（CR） |
|---|---|---|---|
| Customer Amount receive from NymCard (AED) | 从 NymCard 收到的总额 | 0040 | Client Customer Funds |
| Customer Amount to Settle (AED) | 需与 MasterCard 清算的金额 | Client Customer Funds | Settle Pending |
| Customer Amount to Profit (AED) | 需划入利润的金额 | Client Customer Funds | Merchant Basic Account |

> 与 MasterCard 的最终清算动作（Settle with MasterCard）暂为 TODO。

## 余额对账

- NymCard 向 Client 与 PayBy 提供卡余额数据。
- PayBy 按 AED 总额维度进行余额对账。

## 每日清算流程

每日清算流程在原文中列出但未展开细节，需结合上述 FX、卡交易与余额对账三条主线按日切执行。

```
