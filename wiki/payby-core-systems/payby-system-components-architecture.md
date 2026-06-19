---
title: PayBy系统组件架构图
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a707e29e-e063-4661-98b3-218972a81847
tags: []
---

# PayBy系统组件架构图

本页给出 PayBy 支付平台的组件分层视图，展示各服务所属的层级分组、改造状态以及核心依赖关系。

## 图例说明

- **内部应用**：标记为 `a`，浅青色
- **内部管理**：标记为 `a`，浅青色
- **未改造**：标记为 `M`，粉红色（表示尚未完成改造的服务）

## 分层组件清单

### 应用公共
- `paycode`
- `pns`

### 中台公共
- `pbs`
- `limit`

### 通用
- `acs`
- `csa`（未改造）
- `voucher`
- `mns`（未改造）
- `nffs`
- `ma`
- `outman`
- `dpm`

### 运营管理
- `counter`
- `basis`

## 组件依赖关系

以虚线依赖箭头（`-->`）表示：

- `pns` → `acs`
- `paycode` → `ma`（指向 `nffs` 区域）
- `limit` → `ma`
- `pbs` / `limit` → `nffs`
- `ma` → `outman`
- `ma` → `dpm`

## 架构概览

- 依赖方向整体由 **应用公共 / 中台公共** 层流向 **通用** 层（如 `acs`、`ma`、`nffs` 等）
- 通用层中的 `ma` 进一步依赖底层的 `outman` 与 `dpm`
- 图中通过颜色区分已改造组件与 **未改造**（`csa`、`mns`）组件，便于识别平台改造进度
