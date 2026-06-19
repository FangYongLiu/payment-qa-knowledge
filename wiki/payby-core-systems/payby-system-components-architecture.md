---
title: PayBy系统组件架构
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9cd1ad42-cfa4-4c45-939b-7ea82e7ab1d6
tags: []
---

# PayBy系统组件架构

PayBy 核心系统按职责自上而下划分为 **交易 / 支付 / 会员账户 / 资金渠道 / 银行** 五大分层，每层包含若干组件，组件之间通过依赖调用串联起一笔资金从交易发起到银行渠道落地的完整链路。

## 组件类型图例

组件按部署与归属状态分为三类：

- `<<component>> 内部应用`（浅青色）：PayBy 内部已部署的应用。
- `<<component>> 未部署`（红色）：尚未部署的内部应用。
- `<<component>> 合作方应用`（白色）：外部合作方提供的应用。

## 系统分层与组件清单

按从上游业务到下游渠道的顺序，五个分层及其包含的组件如下：

### 交易（Trade）

内部应用：
- `trade`
- `deposit`
- `fundout`
- `cashesk`
- `authpay`
- `query`

### 支付（Payment）

内部应用：
- `pfs-payment`
- `payment`

### 会员账户（Member Account）

内部应用：
- `ma`
- `dpm`

### 资金渠道（Fund Channel）

- 内部应用：`cmf`、`fundchannel-mock`、`fundchannel-xxx`
- 未部署：`fcw`

### 银行（Bank）

- 合作方应用：`bank`

## 组件间依赖关系

主链路（交易 → 支付 → 资金渠道 → 银行）：

- `trade` → `pfs-payment`
- `pfs-payment` → `payment`
- `payment` → `cmf`
- `fundchannel-xxx` → `bank`

交易层内部及上行到支付层的关系：

- `交易` 中的 `trade`、`deposit`、`cashesk` 等多个组件汇聚指向 `pfs-payment`。
- `cashesk` → `authpay`（向下调用）。
- `fundout` / `cashesk` 与 `deposit` 之间存在回向依赖。

支付层到会员账户层：

- `pfs-payment` → `ma`
- `payment` → `dpm`
- `ma` → `dpm`

资金渠道层内部及与银行/未部署组件的关系：

- `cmf` → `fundchannel-mock`
- `cmf` ↔ `fundchannel-xxx`（双向）
- `bank` ⇢ `fcw`（虚线依赖）
- `fcw` ↔ `cmf`（`fcw` 反向接入资金渠道）

## 解读要点

- **分层调用方向**：调用整体自左向右、自上而下，即 交易 → 支付 → 会员账户 / 资金渠道 → 银行，体现"业务交易 → 支付编排 → 账户记账 / 渠道出入金 → 外部银行"的资金流转路径。
- **`pfs-payment` 是支付层入口**：交易层多个组件（`trade`、`deposit`、`cashesk` 等）均汇聚到 `pfs-payment`，再由其下钻到 `payment` 与 `ma`。
- **`cmf` 是资金渠道枢纽**：对接 `fundchannel-mock`、`fundchannel-xxx` 以及未部署的 `fcw`，由 `fundchannel-xxx` 真正对接合作方 `bank`。
- **未部署组件 `fcw`**：与 `cmf` 双向连接、并接收来自 `bank` 的依赖，但当前尚未部署，属于规划中的资金渠道相关组件。
