---
title: Nublo持卡人加载与对账流程
domain: ppc-card-business
kind: wiki_page
slug: nublo-cardholder-loading-flow
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/564101170
tags: []
---

# Nublo持卡人加载与对账流程

本页聚焦Nublo项目中持卡人(Cardholder)加载资金的系统时序、三种预付资金维护方案对比，以及加载对账文件结构与PayBy/Client在对账后的资金调拨动作。FX与卡交易清算见 [[nublo-fx-and-transaction-settlement]]；整体资金流上下文见 [[pcbs-ra-2406-nublo-deprecated]]。

## 加载系统时序 (Loading system sequence)

针对预付资金(pre-funding)由谁维护，存在三种方案：

- **Solution 1**：NymCard 在加载前检查并维护 pre-funding。
- **Solution 2**：由 Client 自行维护。
- **Solution 3**：无任何方任何一方维护。

### 方案对比

| 维度 | Solution 1 👍 | Solution 2 👎 | Solution 3 👎 |
|---|---|---|---|
| 额外集成 (Extra Integration) | ✔ 无需集成 | ✖ 每个 client 都需集成 | ✔ 无需集成 |
| 预付资金不足时的加载体验 | ✖ 加载时校验 | ✖ 加载时校验 | ✔ 不校验 |
| 流动性风险 (Liquidity risk) | ✔ 无风险 | ✔ 或 ✖，取决于 client 实现 | ✖ 若 pre-funds 不足则有风险 |

结论：推荐 Solution 1。

## 加载对账 (Loading reconciliation)

### 前置账户 (Prerequisite)

需要在 Client 名下新增两类账户：

| Belong To | New Account Type | Purpose |
|---|---|---|
| Client | `PCBS_PREFUNDING` | 加载用预付资金账户 |
| Client | `PCBS_ESCROW` | 持卡人资金总账(Total cardholder funds) |

### 对账文件样例

NymCard 向 Client 和 PayBy 提供 loading reconciliation 文件，需包含字段：

- Loading Order ID
- Customer ID
- Loading Amount (AED)
- Submit Time
- Finish Time

### Action 1 — PayBy move to escrow

PayBy 将资金从 pre-funding 划转至 escrow 账户：

- **DR**: `PCBS_PREFUNDING`
- **CR**: `PCBS_ESCROW`

### Action 2 — Client fill up pre-funding

Client 按对账金额将资金转入 PayBy 指定 IBAN(归属 Client)，PayBy 将其入账到 client pre-funding：

- **DR**: `0040`
- **CR**: `PCBS_PREFUNDING`

## 余额对账 (Balance reconciliation)

- NymCard 向 client 和 PayBy 提供卡余额数据。
- PayBy 按 AED 总额做余额对账。
