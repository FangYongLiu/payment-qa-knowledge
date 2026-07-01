---
title: PCBS RA-2406 Nublo方案总览(已废弃)
domain: ppc-card-business
kind: wiki_page
slug: pcbs-ra-2406-nublo-deprecated-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:59c0c97d-afe6-440e-b5d9-9a6333b05ae3
tags: []
---

# PCBS RA-2406 Nublo方案总览(已废弃)

> ⚠️ 本页为 Nublo BIN Sponsorship 方案的存档版本，已废弃。仅作为历史参考。

本页概述 Nublo BIN Sponsorship 项目下的整体资金流、持卡人加载、外汇、卡交易、对账与日终结算的总体框架。具体细节见 [[nublo-cardholder-loading-reconciliation]] 与 [[nublo-fx-and-card-transaction-settlement]]。

## 资源与参考

- PRD: Bin Sponsorship Flow
- 资金流(Funds Flow)示意见原文附图

## 持卡人加载 (Cardholder Loading)

### 加载系统时序方案对比

| 方案 | 描述 | Extra Integration | 加载体验(预存不足时) | 流动性风险 |
|---|---|---|---|---|
| Solution 1 👍 | NymCard 在加载前检查并维护 pre-funding | ✔ 无需集成 | ✖ 加载时校验 | ✔ 无风险 |
| Solution 2 👎 | 由 Client 自行处理 | ✖ 每个 Client 都需集成 | ✖ 加载时校验 | 取决于 Client 实现 |
| Solution 3 👎 | 无方任何方处理 | ✔ 无需集成 | ✔ 不校验 | ✖ pre-funds 不足时存在风险 |

### 加载对账概要

- 新增账户类型：
  - `PCBS_PREFUNDING`(Client)：加载预存资金
  - `PCBS_ESCROW`(Client)：持卡人总资金
- NymCard 向 Client 与 PayBy 提供加载对账文件
- 两类资金动作：
  - **Action 1**：PayBy 从 pre-funding 划转至 escrow，DR `PCBS_PREFUNDING` / CR `PCBS_ESCROW`
  - **Action 2**：Client 转入 PayBy 指定 IBAN 补足 pre-funding，DR `0040` / CR `PCBS_PREFUNDING`

详见 [[nublo-cardholder-loading-reconciliation]]。

## 外汇 (Foreign Exchange)

- Client 仅与 NymCard 集成
- NymCard 向 Client 与 PayBy 提供 FX 对账文件
- 根据方向进行资金划转：
  - AED → Foreign：PayBy 将总 AED 金额转给 NymCard
  - Foreign → AED：PayBy 从 NymCard 接收总 AED 金额
  - `Profit Amount (AED)`：从 Escrow Account 划至 Profit Account

详见 [[nublo-fx-and-card-transaction-settlement]]。

## 卡交易 (Card Transaction)

- Client 仅与 NymCard 集成
- NymCard 向 Client 与 PayBy 提供交易对账文件
- 结算动作：
  - NymCard 按结算币种把金额转给 PayBy
  - PayBy 按需将 AED 与 USD 金额转给 MC
  - PayBy 将利润(fees 与 interchange)划入 Client basic account
- 关键金额拆分：Wallet Amount / Settlement Amount / Profit Amount
- 三笔账务分录：
  - `Customer Amount receive from NymCard (AED)`：DR `0040` / CR `Client Customer Funds`
  - `Customer Amount to Settle (AED)`：DR `Client Customer Funds` / CR `Settle Pending`
  - `Customer Amount to Profit (AED)`：DR `Client Customer Funds` / CR `Merchant Basic Account`
- 待办：与 MasterCard 结算 (TODO)

详见 [[nublo-fx-and-card-transaction-settlement]]。

## 余额对账 (Balance Reconciliation)

- NymCard 向 Client 与 PayBy 提供卡余额数据
- PayBy 在总账层面进行 AED 余额对账

## 日终结算流程 (Daily Settlement Flow)

按上述加载、FX、卡交易三大模块对应的对账文件与资金动作汇总执行。

---

*备注：本方案已废弃，后续以新版方案替代。*
