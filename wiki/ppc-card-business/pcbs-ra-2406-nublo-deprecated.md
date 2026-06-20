---
title: PCBS RA-2406 Nublo项目资金流程(已废弃)
domain: ppc-card-business
kind: wiki_page
slug: pcbs-ra-2406-nublo-deprecated
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/564101170
tags: []
---

# PCBS RA-2406 Nublo项目资金流程(已废弃)

> ⚠️ 本页所述方案已废弃，仅作历史归档参考。

本页汇总 Nublo 项目通过 NymCard 发卡的端到端资金流程总览：从持卡人加载、外汇、卡交易、清算到余额对账各环节的方案选型与账务动作。详细子流程见 [[nublo-cardholder-loading-flow]] 与 [[nublo-fx-and-transaction-settlement]]。

## 资源与参考
- PRD: Bin Sponsorship Flow
- 资金流向图（Funds Flow）

## 持卡人加载 (Cardholder Loading)

### 方案对比
预资金（pre-funding）维护方式三种方案：

| 方案 | 描述 | 额外集成 | 预资金不足时加载体验 | 流动性风险 |
|---|---|---|---|---|
| Solution 1 👍 | NymCard 在加载前检查并维护预资金 | ✔ 无需集成 | ✖ 加载校验 | ✔ 无风险 |
| Solution 2 👎 | Client 自行处理 | ✖ 每个客户都需集成 | ✖ 加载校验 | 取决于客户实现 |
| Solution 3 👎 | 无任何方处理 | ✔ 无需集成 | ✔ 不校验 | ✖ 预资金不足即风险 |

最终选型：**Solution 1**。

### 加载对账前置账户
| Belong To | New Account Type | Purpose |
|---|---|---|
| Client | PCBS_PREFUNDING | Loading pre-funding |
| Client | PCBS_ESCROW | Total cardholder funds |

### 对账文件字段
NymCard 向 Client 与 PayBy 提供 Loading 对账文件，包含：
- Loading Order ID
- Customer ID
- Loading Amount (AED)
- Submit Time
- Finish Time

### 账务动作
- **Action 1 — PayBy 移至 Escrow**：将预资金转入 escrow
  - DR: `PCBS_PREFUNDING`
  - CR: `PCBS_ESCROW`
- **Action 2 — Client 补充预资金**：Client 转账至 PayBy 指定 IBAN（归属 Client），PayBy 入账至预资金账户
  - DR: `0040`
  - CR: `PCBS_PREFUNDING`

详见 [[nublo-cardholder-loading-flow]]。

## 外汇 (Foreign Exchange)

- 系统集成：Client 仅与 NymCard 对接。
- NymCard 向 Client 与 PayBy 提供 FX 对账文件。
- 资金调拨方向：
  - AED → 外币：将总 AED 金额划转给 NymCard
  - 外币 → AED：从 NymCard 收取总 AED 金额
- **Profit Amount (AED)**：从 Escrow Account 移至 Profit Account。
- PayBy 与 NymCard 之间根据需要互转，用于 hedging tuning。

### FX 对账字段
- FX Order ID
- Customer ID
- From Currency / From Amount
- To Currency / To Amount
- Profit Amount (AED)

## 卡交易 (Card Transaction)

- 卡交易流程：Client 仅与 NymCard 对接。
- 清算文件由 NymCard 提供给 Client 与 PayBy。

### 清算资金流（外币部分）
1. NymCard 按结算币种将金额转给 PayBy。
2. PayBy 按相应金额转 AED 与 USD 给 MC（MasterCard）。
3. PayBy 将利润（fees 与 interchange）移至 Client basic account。

### 交易对账字段
- Transaction ID
- Customer ID
- Wallet Currency / Wallet Amount
- Customer Amount receive from NymCard (AED)
- Customer Amount to Settle (AED)
- Customer Amount to Profit (AED)
- Settlement Currency / Settlement Amount
- Transaction Time / Settlement Date / Settlement Cycle

### 账务动作
- **Customer Amount receive from NymCard (AED)** — 从 NymCard 收入总额
  - DR: `0040`
  - CR: `Client Customer Funds`
- **Customer Amount to Settle (AED)** — 与 MasterCard 结算的金额
  - DR: `Client Customer Funds`
  - CR: `Settle Pending`
- **Customer Amount to Profit (AED)** — 划转作为利润的金额
  - DR: `Client Customer Funds`
  - CR: `Merchant Basic Account`
- TODO: Settle with MasterCard

详见 [[nublo-fx-and-transaction-settlement]]。

## 余额对账 (Balance Reconciliation)

- NymCard 向 Client 与 PayBy 提供卡余额数据。
- PayBy 在总账层面进行 AED 余额对账。

## 每日清算流程 (Daily Settlement Flow)

每日清算流程汇总以上加载、FX、卡交易、余额对账各环节资金动作（原文章节 7.1，未展开）。
