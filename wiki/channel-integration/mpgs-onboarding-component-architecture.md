---
title: MPGS Onboarding组件架构与依赖关系
domain: channel-integration
kind: wiki_page
slug: mpgs-onboarding-component-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:c2d176f8-25d1-4750-bf00-2a53a12f317a
tags: []
---

# MPGS Onboarding组件架构与依赖关系

本页描述 MPGS Onboarding 方案中 `basis`、`onboarding`、`ppcenter`、`cmf`、`qpay-ni` 五个组件之间的调用与依赖关系。

## 组件清单

- **basis**：上层基础组件
- **onboarding**：入网核心组件
- **ppcenter**：被 onboarding 调用的下游组件
- **cmf**：与 onboarding 双向交互的组件
- **qpay-ni**：被 cmf 调用，并回调 onboarding 的组件

## 依赖关系

依赖方向表示「调用 / 依赖」：

- `basis` → `onboarding`
- `onboarding` → `ppcenter`
- `onboarding` → `cmf`
- `cmf` → `onboarding`（与上一条共同构成双向依赖）
- `cmf` → `qpay-ni`
- `qpay-ni` → `onboarding`

## 拓扑结构

- `basis` 位于顶层，向下依赖 `onboarding`
- `onboarding` 居于中部，是整体交互的核心节点：向右调用 `ppcenter`，与下方 `cmf` 双向交互
- `cmf` 位于 `onboarding` 下方，进一步向下调用 `qpay-ni`
- `qpay-ni` 位于最底层，并通过一条回路（沿左侧）回调到 `onboarding`，形成 `onboarding → cmf → qpay-ni → onboarding` 的闭环
