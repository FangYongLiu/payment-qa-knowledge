---
title: Nublo持卡人加载与对账方案
domain: ppc-card-business
kind: wiki_page
slug: nublo-cardholder-loading-reconciliation
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:59c0c97d-afe6-440e-b5d9-9a6333b05ae3
tags: []
---

# Nublo持卡人加载与对账方案

本页聚焦Nublo方案中持卡人加载（Cardholder Loading）的系统时序、pre-funding三种方案对比，以及加载对账文件样本和PayBy/Client侧的资金动作。FX与卡交易部分见 [[nublo-fx-and-card-transaction-settlement]]，整体方案背景见 [[pcbs-ra-2406-nublo-deprecated-overview]]。

## 加载系统时序

Client 与 NymCard 集成完成持卡人加载流程，pre-funding 的检查与维护由不同方承担，对应三种解决方案。

## Pre-funding 三种方案对比

| 维度 | Solution 1 (NymCard维护) | Solution 2 (Client维护) | Solution 3 (无人维护) |
|---|---|---|---|
| 总体评价 | 👍 | 👎 | 👎 |
| 额外集成 | ✔ 无需集成 | ✖ 每个 client 都需集成 | ✔ 无需集成 |
| Pre-funds 不足时的加载体验 | ✖ 加载时校验 | ✖ 加载时校验 | ✔ 不校验 |
| 流动性风险 | ✔ 无风险 | ✔/✖ 取决于 client 实现 | ✖ Pre-funds 不足时存在风险 |

- Solution 1：NymCard 在加载前检查并维护 pre-funding。
- Solution 2：由 Client 自行处理。
- Solution 3：无方维护。

## 加载对账

### 前置账户

| Belong To | New Account Type | Purpose |
|---|---|---|
| Client | `PCBS_PREFUNDING` | Loading pre-funding |
| Client | `PCBS_ESCROW` | Total cardholder funds |

### 对账文件样本

NymCard 向 Client 和 PayBy 提供加载对账文件，必须包含以下字段：

- Loading Order ID
- Customer ID
- Loading Amount (AED)
- Submit Time
- Finish Time

### Action 1 - PayBy move to escrow

PayBy 将资金从 pre-funding 转入 escrow 账户：

- DR: `PCBS_PREFUNDING`
- CR: `PCBS_ESCROW`

### Action 2 - Client fill up pre-funding

Client 将相应金额转账至 PayBy 指定 IBAN（归属 Client），PayBy 将该金额贷记到 client pre-funding 账户：

- DR: `0040`
- CR: `PCBS_PREFUNDING`
