---
title: Nublo项目资金流架构图(已废弃)
domain: ppc-card-business
kind: wiki_page
slug: pcbs-ra-2406-nublo-deprecated-funds-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b1ee856c-671d-497e-a8a4-02735e769049
tags: []
---

# Nublo项目资金流架构图(已废弃)

> ⚠️ 本页内容已废弃，仅作历史归档参考。

本页描述 Nublo 卡项目中持卡人、Client App、Payby 托管账户与 NymCard 之间的资金流转关系（Funds Flow）。

## 参与方

资金流涉及四个参与方，按泳道从左到右排列：

- **Cardholder**：持卡人
- **Client / Client App**：客户端应用
- **Payby**：托管与结算账户持有方
- **NymCard**：发卡与清结算运营方

## Cardholder 泳道

- Daily Loads from Cardholders（持卡人每日充值）
- Daily Card Spends by Cardholders（持卡人每日卡消费）

## Client / Client App 泳道

- Loading Channels（充值通道）
- Card（卡）

## Payby 泳道（账户与流程）

Payby 侧维护三个账户，按以下顺序流转：

### Loads Collection Bank Account - AED（充值归集账户）

1. Daily Reconciliation of Loads Received（每日对账已收充值）
2. Move Loads into Escrow Bank Account（将充值划入托管账户）

### Cardholder Funds Bank Account (Escrow) - AED（持卡人资金托管账户）

3. Cardholder Spend Debited on a daily basis in AED and Credited to Client Prefunded Account with NymCard（每日以 AED 借记持卡人消费金额，并贷记到 NymCard 的 Client Prefunded Account）

> 0. Pre-Going Live：Client 在上线前向 NymCard 的 Prefunded Account 预存资金，用于支持结算所需的 FX 操作。

### Scheme Settlement Account - MultiCurrency（多币种卡组织结算账户）

7. Daily Net Cardholder Spend in AED and Foreign Currencies (As accepted by Scheme) - Interchange + Scheme Fees（每日净持卡人消费，按卡组织接受的 AED 及外币结算，扣除 Interchange + Scheme Fees）

> Transaction and Balance Reports provided by NymCard（交易及余额报表由 NymCard 提供）

## NymCard 泳道

**NymCard Ops**：

- Ongoing - Daily Hedging on Currency Open Positions（持续进行的每日货币敞口对冲）
- Daily FX Conversions to support multicurrency settlements（每日 FX 转换，支持多币种结算，按 Scheme 接受的币种）

## 关键点

- 充值资金路径：Cardholder → Loading Channels → Loads Collection Account (AED) → Escrow Account (AED)
- 消费结算路径：Escrow Account (AED) → Client Prefunded Account @ NymCard → Scheme Settlement Account (MultiCurrency)
- FX 风险由 NymCard Ops 通过每日对冲与每日 FX 转换处理
- 上线前需由 Client 完成 Prefund，以保障 FX 与结算运营
