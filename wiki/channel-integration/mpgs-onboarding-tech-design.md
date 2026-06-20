---
title: MPGS Onboarding 技术方案设计
domain: channel-integration
kind: wiki_page
slug: mpgs-onboarding-tech-design
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:6e07ad6b-9dd4-4ed3-aa7d-4c541d9eca23
tags: []
---

# MPGS Onboarding 技术方案设计

本页基于 UML 类图说明 MPGS 渠道 Onboarding 的领域模型与 Facade 接口设计，核心是以 `ItemIndex` 为键的 `OnboardingItem`，并通过两个 Facade 分别承担读取与注册/重试职责。

## 领域模型

### OnboardingItem
表示一个 Onboarding 实体，承载渠道侧注册结果与状态。

- `fundProviderCode: string`
- `ownerId: string`
- `resultParamMap: map<string,string>`
- `status: OnboardingItemStatus`
- `type: ItemType`

### ItemIndex
`OnboardingItem` 的复合索引键，用于唯一定位一个 Item。

- `fundProviderCode: string`
- `ownerId: string`
- `type: ItemType`

### ItemRegistrationInfo
注册入参载体，按 `ItemIndex` 维度组织注册参数。

- `registrationInfoMap: map<ItemIndex, Map<string,string>>`

## Facade 接口

### OnboardingItemFacade
读取侧 Facade，负责按索引查询 Item。

- `getItem(ItemIndex): OnboardingItem`

### OnboardingFacade
写入侧 Facade（图中拼写为 `OnbaordingFacade`），负责注册与重试。

- `registerItem(ItemRegistrationInfo): boolean`
- `retry(ItemIndex): void`

## 关键关系

- `OnboardingItem` 由 `ItemIndex`（`fundProviderCode` + `ownerId` + `ItemType` 组合）唯一定位。
- `OnboardingItemFacade.getItem` 入参为 `ItemIndex`，返回 `OnboardingItem`。
- `OnboardingFacade.registerItem` 入参为 `ItemRegistrationInfo`；`retry` 入参为 `ItemIndex`。
- `OnboardingItem` 与 `ItemIndex` 在类图中存在向上延伸的关联线，提示存在未在本图展示的父类/关联类。
