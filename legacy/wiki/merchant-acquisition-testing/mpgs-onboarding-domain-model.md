---
title: MPGS Onboarding 领域模型设计
domain: merchant-acquisition-testing
kind: wiki_page
slug: mpgs-onboarding-domain-model
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:c28c1c91-22f6-48b5-8de4-51c52d068d09
tags: []
---

# MPGS Onboarding 领域模型设计

本页描述 MPGS 入驻方案的 UML 类图设计，包含核心领域对象 `RegisterItem`、`OnboardingItem`、`ItemIndex`，以及对外暴露的 Facade 接口。

## 枚举定义

### ItemType
入驻对象的类型，三个层级：
- `MERCHANT`
- `STORE`
- `DEVICE`

### OnboardingItemStatus
入驻处理项的状态枚举（具体取值未在类图中列出）。

## 核心领域对象

### RegisterItem（基类）
注册项的抽象基类，承载注册所需的通用信息。

字段：
- `fundProviderCode: string`
- `ownerId: string`
- `resultParamMap: map<string,string>`
- `type: ItemType`

### OnboardingItem
入驻处理项，继承自 `RegisterItem`，并带有处理状态。

字段：
- `fundProviderCode: string`
- `ownerId: string`
- `resultParamMap: map<string,string>`
- `status: OnboardingItemStatus`
- `type: ItemType`

### ManualRegisterItem
手动注册项，继承自 `RegisterItem`（类图中未列出额外字段）。

### ItemIndex
用于定位某个 Item 的索引对象。

字段：
- `fundProviderCode: string`
- `ownerId: string`
- `type: ItemType`

## 对外 Facade 接口

### OnboardingItemFacade
- `getItem(ItemIndex): OnboardingItem` — 根据索引获取入驻项。

### OnbaordingFacade
（类图中拼写为 `Onbaording`）
- `manualRegister(ManualRegisterItem): boolean` — 手动注册。
- `retry(ItemIndex): void` — 针对指定索引的入驻项发起重试。

## 关系总览

- 继承关系：`OnboardingItem` 与 `ManualRegisterItem` 均继承自 `RegisterItem`。
- 关联关系：`OnboardingItem`、`ItemIndex`、`RegisterItem` 都引用枚举 `ItemType`；`OnboardingItem` 通过 `status` 字段引用 `OnboardingItemStatus`。
- 依赖关系：`OnboardingItemFacade` 依赖 `ItemIndex` 与 `OnboardingItem`，作为入参与返回值。
