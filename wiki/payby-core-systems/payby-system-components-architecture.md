---
title: PayBy系统组件架构总览
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9f7fc10d-b291-4cb3-8cb9-3f6f5a81cd40
tags: []
---

# PayBy系统组件架构总览

本页基于 UML 组件图描述 PayBy 支付系统的整体模块划分与依赖关系，包含 **交易 / 支付 / 会员账户 / 资金渠道 / 银行** 5 大 package，以及各 package 内部的应用组件与跨包调用链路。

## 组件类型图例

组件按颜色区分为三类：

- **内部应用** `<<component>>`（蓝色）：PayBy 自研、已完成改造的应用。
- **未改造** `<<component>>`（红色）：尚未完成改造的内部组件。
- **合作方应用** `<<component>>`（白色）：外部合作方系统。

## 5 大 Package 与内部组件

### 交易 (Trade)

内部应用：

- `trade`
- `deposit`
- `fundout`
- `cashesk`
- `authpay`

### 支付 (Payment)

内部应用：

- `pfs-payment`
- `payment`

### 会员账户 (Member Account)

- 内部应用：`ma`、`dpm`
- 未改造：`cdpm`

### 资金渠道 (Fund Channel)

内部应用：

- `cmf`
- `fundchannel-mock`
- `fundchannel-xxx`
- `fcw`

### 银行 (Bank)

- 合作方应用：`bank`

## 主要依赖关系

### 交易包内部

- `cashesk` → `authpay`
- `deposit`、`fundout` 与 `cashesk`、`trade` 相互关联
- `authpay` 与 `cashesk` 关联

### 交易 → 支付

- `trade` → `pfs-payment`
- `deposit`、`fundout`、`cashesk` 反向引用至 `pfs-payment` / `trade`

### 支付包内部及向会员账户

- `pfs-payment` → `payment`
- `pfs-payment` ↔ `ma`
- `payment` → `dpm`
- `dpm` → `cdpm`
- `ma` → `dpm`

### 支付 → 资金渠道

- `payment` → `cmf`
- `cmf` → `fundchannel-mock`
- `cmf` → `fcw`

### 资金渠道 ↔ 银行

- `fundchannel-xxx` → `bank`
- `bank` → `fcw`（回调）

## 整体调用链路

主流程自上而下贯通：

`trade` → `pfs-payment` → `payment` → 会员账户域（经 `ma` 进入 `dpm` / `cdpm`）+ 资金渠道域（`cmf` → `fundchannel-xxx` → `bank`，并由 `bank` 回调 `fcw`）。
