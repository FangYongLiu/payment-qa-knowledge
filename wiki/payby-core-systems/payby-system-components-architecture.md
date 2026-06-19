---
title: PayBy系统组件架构图
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:6306e63f-2247-48c0-831c-938438b74455
tags: []
---

# PayBy系统组件架构图

本页基于系统组件图，梳理 PayBy 支付平台各业务模块的组件构成及其依赖关系，整体呈现"交易接入 → 支付编排 → 会员账务 / 资金渠道 → 银行 → 监管"的分层调用链路。

## 顶层接入组件

位于架构图最外层、未归属具体 package 的接入层组件：

- Inner Service
- Inner Console
- Partner Service

## 业务模块组件清单

### Trade（交易域）

- tradeii
- deposit
- fundout
- cashesk
- authpay
- query

### Payment（支付域）

- pfs-payment
- payment

### Member & Account（会员与账务域）

- ma
- dpm

### Fund Channel（资金渠道域）

- cmf
- fundchannel-xxx
- fundchannel-yyy
- router
- fcw

### Bank（银行域）

- bank

### Operation Support（运营支撑域）

- counter
- reconciliation
- counter（图中存在第二个同名 counter 组件）

### Regulation（监管域）

- escrow

## 组件依赖关系

以下依赖关系来自组件图中的虚线箭头（`«component»` dependency）。

### Trade → Payment

- tradeii → pfs-payment
- cashesk 与 pfs-payment 区域相连，并与 deposit / fundout 组件存在关联
- cashesk → authpay

### Payment 内部及其向下依赖

- pfs-payment → payment
- pfs-payment → ma
- payment → cmf
- payment → dpm

### Member & Account 内部

- ma → dpm

### Fund Channel 内部及与 Bank 的交互

- cmf → fundchannel-xxx
- cmf ↔ router
- fundchannel-yyy ↔ router
- fundchannel-yyy → bank（同时存在 bank ← fundchannel 方向的反向箭头）
- router ← bank
- fcw ↔ cmf / bank（fcw 向上连接至 Fund Channel，并与 bank 相连）

### Regulation 依赖 Bank

- escrow ← bank（监管域依赖银行域）

## 整体调用流向

整体由 Trade 层服务（如 tradeii、cashesk 等）向下经 Payment 层（pfs-payment、payment）进行支付编排，再分别落到：

- Member & Account（ma / dpm）完成会员与账务处理
- Fund Channel（cmf、router、fundchannel-xxx/yyy、fcw）完成资金渠道路由
- 最终通过 Bank（bank）对接外部银行
- Regulation（escrow）依赖 Bank 实现监管资金存管

Operation Support（counter、reconciliation）作为运营支撑独立成域，服务于上述核心链路。
