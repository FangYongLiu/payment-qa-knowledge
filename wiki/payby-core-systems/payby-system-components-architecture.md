---
title: PayBy支付系统组件架构图
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:05618283-25e8-4ee4-afc4-ccecd636f160
tags: []
---

# PayBy支付系统组件架构图

本页描述 PayBy 支付系统的组件分层与依赖关系，整体由五个包组成：**交易、支付、会员账户、资金渠道、银行**。交易层应用通过 `pfs-payment` 进行编排，向下调用支付、会员账户与资金渠道，最终对接银行。

## 组件类型图例

组件按颜色区分三类：

- `<<component>> 内部应用`（浅青色）
- `<<component>> 未改造`（粉红色）
- `<<component>> 合作方应用`（白色）

## 分层包与组件清单

按从上到下（业务调用方向）划分为五个包：

### 交易（Trade）
- `trade`
- `deposit`
- `fundout`
- `cashesk`
- `authpay`

均为内部应用。

### 支付（Payment）
- `pfs-payment`
- `payment`

均为内部应用。

### 会员账户（Member Account）
- `ma`
- `dpm`

均为内部应用。

### 资金渠道（Fund Channel）
- `cmf`
- `fundchannel-mock`
- `fundchannel-xxx`
- `fcw`

均为内部应用。

### 银行（Bank）
- `bank`（合作方应用）

## 组件依赖关系

### 交易层 → 支付层
- `trade` → `pfs-payment`
- `deposit` → `pfs-payment`
- `cashesk` → `pfs-payment`
- `cashesk` → `authpay`
- `fundout` 连接回交易组 / `pfs-payment` 区域

### 支付层内部与向下调用
- `pfs-payment` → `payment`
- `pfs-payment` → `ma`（下沉到会员账户）
- `payment` → `cmf`
- `payment` → `dpm`

### 会员账户层
- `ma` → `dpm`

### 资金渠道层内部
- `cmf` → `fundchannel-mock`
- `cmf` ↔ `fcw`（双向）
- `fundchannel-mock` → `fundchannel-xxx`

### 资金渠道 → 银行
- `fundchannel-xxx` → `bank`
- `bank` → `fcw`（虚线下行）

## 整体调用流向

交易层应用（`trade` / `deposit` / `cashesk` / `fundout` 等）统一进入 `pfs-payment` 进行编排；`pfs-payment` 一方面驱动 `payment`，由 `payment` 调度 `cmf` 完成资金渠道路由，另一方面下沉到 `ma` 操作会员账户与 `dpm`；资金渠道侧通过 `fundchannel-mock` / `fundchannel-xxx` 最终对接合作方 `bank`，并由 `bank` 回流至 `fcw`。
