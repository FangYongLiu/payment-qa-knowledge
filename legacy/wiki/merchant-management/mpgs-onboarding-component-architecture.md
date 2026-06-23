---
title: MPGS Onboarding组件依赖架构
domain: merchant-management
kind: wiki_page
slug: mpgs-onboarding-component-architecture
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:23a18f70-5fd9-4dcd-86da-3ab35a5a4a27
tags: []
---

# MPGS Onboarding组件依赖架构

本页描述 MPGS Onboarding 技术方案中各组件之间的调用与依赖关系，涉及 `basis`、`onboarding`、`ppcenter`、`cmf`、`qpay-ni` 五个组件。

## 组件清单

- `basis`
- `onboarding`
- `ppcenter`
- `cmf`
- `qpay-ni`

## 依赖关系

以箭头方向表示「依赖 / 调用」：

- `basis` → `onboarding`
- `onboarding` → `ppcenter`
- `onboarding` → `cmf`（与下条构成双向依赖）
- `cmf` → `onboarding`
- `cmf` → `qpay-ni`
- `qpay-ni` → `onboarding`

## 关键特征

- `onboarding` 与 `cmf` 之间为双向依赖（两条独立的依赖边）。
- `qpay-ni` 反向回调 `onboarding`，与 `basis → onboarding`、`cmf → onboarding` 共同形成多个上游调用入口。
- `ppcenter` 仅作为 `onboarding` 的下游被调用方出现。

## 布局示意

- 顶部：`basis`
- 中部：`onboarding`（左）、`ppcenter`（右）
- `onboarding` 下方：`cmf`
- 底部：`qpay-ni`（位于 `cmf` 下方，并通过左侧长连线回连至 `onboarding`）

> 该关系图以 UML 组件/依赖图形式呈现，用于说明 MPGS Onboarding 模块间的交互架构。
