---
title: PayBy系统组件架构图
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:efd73f03-1b45-46b3-9dd6-029e331019e5
tags: []
---

# PayBy系统组件架构图

本页基于系统架构图，描述 PayBy 平台五大模块（Trade、Payment、Member & Account、Fund Channel、Bank）的组件构成与依赖关系。

## 图例说明

组件按服务类型分为三类：

- **Inner Service**（内部服务）：青色/浅蓝填充
- **Unready**（未就绪）：红色填充
- **Partner Service**（合作方服务）：白色填充

## 模块与组件清单

五个模块自左向右依次为 Trade、Payment、Member & Account、Fund Channel、Bank。

### Trade（交易层）

均为 Inner Service：

- `trade`
- `deposit`
- `fundout`
- `cashesk`
- `authpay`
- `query`

### Payment（支付层）

均为 Inner Service：

- `pfs-payment`
- `payment`

### Member & Account（会员与账户）

均为 Inner Service：

- `ma`
- `dpm`

### Fund Channel（资金通道）

- `cmf`（Inner Service）
- `fundchannel-mock`（Inner Service）
- `fundchannel-xxx`（Inner Service）
- `fcw`（Unready，未就绪）

### Bank（银行）

- `bank`（Partner Service，合作方服务）

## 组件依赖关系

各组件之间的调用与依赖（虚线依赖箭头）如下：

### Trade → Payment

- `trade` → `pfs-payment`
- `deposit`、`fundout`、`cashesk` → `pfs-payment`（Trade 层服务汇入 `pfs-payment`）
- `cashesk` → `authpay`

### Payment 内部及向下游

- `pfs-payment` → `payment`
- `payment` → `cmf`

### Payment → Member & Account

- `pfs-payment` → `ma`
- `payment` → `dpm`
- `ma` → `dpm`

### Fund Channel 内部及向 Bank

- `cmf` → `fundchannel-mock`
- `cmf` ↔ `fcw`（双向）
- `fundchannel-xxx` → `bank`
- `bank` → `fcw`
- `bank` → `fundchannel-xxx`（返回链路）

## 整体调用流

Trade 层服务调用 Payment 层（`pfs-payment`、`payment`），Payment 层进一步依赖 Member & Account 层（`ma`、`dpm`）以及 Fund Channel 层（`cmf` 等），最终通过 Fund Channel 对接 Bank（合作方）完成资金侧交互。
