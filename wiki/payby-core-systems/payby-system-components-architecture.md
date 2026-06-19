---
title: PayBy系统组件架构图
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:1a9eb9ef-3e09-4975-916b-e9f304ed4588
tags: []
---

# PayBy系统组件架构图

本页以 UML 组件图（PlantUML 风格）描述 PayBy 平台的服务包划分及其组件之间的依赖关系，覆盖 Trade、Payment、Member & Account、Fund Channel、Bank、Operation Support、Regulation 七大包及外部接入层。

## 接入层（顶层组件）

位于架构图顶部、未归属任何 package 的对外/对内入口：

- Inner Service
- Inner Console
- Partner Service

这三个组件作为上游调用方，依赖进入 Trade 包内的相关服务。

## 服务包组成

各 package 包含的组件如下（保留原始命名）：

### Trade
- tradeii
- deposit
- fundout
- cashdesk
- authpay
- query

### Payment
- pfs-payment
- payment

### Member & Account
- ma
- dpm

### Fund Channel
- cmf
- fundchannel-xxx
- fundchannel-yyy
- router
- fcw

### Bank
- bank

### Operation Support
- counter
- reconciliation

### Regulation
- escrow

## 组件依赖关系

组件之间以虚线依赖箭头连接，主要链路如下：

### 接入层 → Trade
- Inner Service、Inner Console、Partner Service 共同对接 Trade 包，进入 `tradeii`、`deposit`、`cashdesk`。

### Trade 内部及 Trade → Payment
- `tradeii` → `pfs-payment`
- `cashdesk` → `authpay`
- `cashdesk`、`fundout` 与 `pfs-payment` 交互

### Payment 内部及横向依赖
- `pfs-payment` → `payment`
- `pfs-payment` ↔ `ma`（Member & Account）
- `payment` → `dpm`
- `payment` → `cmf`（进入 Fund Channel）

### Member & Account 内部
- `ma` → `dpm`

### Fund Channel → Bank
- `cmf` → `fundchannel-xxx`
- `cmf` 连接 `fundchannel-yyy` 与 `router`
- `fundchannel-yyy` ↔ `bank`
- `router` ↔ `bank`
- `fcw` 连接 `bank`

## 包级架构概览

- **业务受理层**：Trade 包承接来自 Inner Service / Inner Console / Partner Service 的交易请求（交易、充值、提现、收银台、授权支付、查询）。
- **支付编排层**：Payment 包（`pfs-payment` + `payment`）作为交易与资金渠道之间的支付编排核心，并与会员账户体系联动。
- **会员与账户层**：Member & Account 包（`ma`、`dpm`）提供会员信息与账户/资金处理能力，被 Payment 直接依赖。
- **资金渠道层**：Fund Channel 包通过 `cmf` 汇聚多渠道（`fundchannel-xxx`、`fundchannel-yyy`）与 `router`、`fcw`，对接 Bank。
- **银行接入层**：Bank 包内 `bank` 组件是渠道与外部银行交互的统一接入点。
- **运营支撑**：Operation Support 包提供 `counter`（计数）与 `reconciliation`（对账）能力。
- **监管合规**：Regulation 包包含 `escrow`（备付金/托管）组件。

> 注：以上组件命名、包归属与依赖方向均依据系统组件图原图（image2021-6-21_11-18-53.png），未做改写。
