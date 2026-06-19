---
title: PayBy系统组件分层架构
domain: payby-core-systems
kind: wiki_page
slug: payby-system-components-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:872324a2-2fb1-4453-b3ce-d0df32b0e25a
tags: []
---

# PayBy系统组件分层架构

本页描述 PayBy 核心系统的组件分层划分及组件之间的依赖关系，分层包括顶层内部服务、App Public、Payment Public、Common 与 Operation Support 五个分组。

## 分层与组件清单

### 顶层（Inner）
- `Inner Service`
- `Inner Console`

### App Public
- `pcs`
- `pns`

### Payment Public
- `pbs`
- `limit`

### Common
- `acs`
- `mns`
- `voucher`
- `nffs`
- `ma`
- `outman`
- `dpm`

### Operation Support
- `counter`
- `basis`
- `csc`
- `sqlmonitor`

## 组件依赖关系

App Public 与 Payment Public 层主要消费 Common 层提供的服务，其中 `ma` 进一步依赖 `outman` 与 `dpm`。

跨层依赖：
- `pns` → `acs` （App Public → Common）
- `pcs` → `ma` （App Public → Common）
- `limit` → `ma` （Payment Public → Common）
- `pbs` → `nffs` （Payment Public → Common）

Common 内部依赖：
- `ma` → `outman`
- `ma` → `dpm`

## 说明

- Common 中的 `mns`、`voucher` 以及 `acs` 在图中除上述指向外未画出其他出向依赖。
- Operation Support 层（`counter`、`basis`、`csc`、`sqlmonitor`）作为独立支撑模块，图中未绘制依赖箭头。
