---
title: MPGS Onboarding技术方案
domain: channel-integration
kind: wiki_page
slug: mpgs-onboarding-tech-design
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:786a9371-2403-41c9-a05a-6ee477a01aab
tags: []
---

# MPGS Onboarding技术方案

本页描述 MPGS 渠道入驻（Onboarding）的领域模型与 Facade 接口设计，用于支撑入驻信息的注册、查询与重试。

## 领域模型

### OnboardingItem
表示一个入驻条目（实体）。

- `fundProviderCode: string`
- `ownerId: string`
- `resultParamMap: map<string, string>`
- `status: OnboardingItemStatus`
- `type: ItemType`

### ItemIndex
入驻条目的索引/查询键。

- `fundProviderCode: string`
- `ownerId: string`
- `type: ItemType`

### ItemRegistrationInfo
入驻注册信息，按 `ItemType` 聚合多类结果参数。

- `fundProviderCode: string`
- `ownerId: string`
- `resultMap: map<ItemType, Map<string, string>>`

## Facade 接口

### OnboardingItemFacade
提供单条入驻条目的查询能力。

- `getItem(ItemIndex): OnboardingItem`

### OnboardingFacade
提供入驻注册与重试能力。

- `register(ItemRegistrationInfo): boolean`
- `retry(ItemIndex): void`

## 依赖关系

- `OnboardingItemFacade` 依赖 `ItemIndex`（入参）与 `OnboardingItem`（返回值）。
- `OnboardingFacade` 依赖 `ItemRegistrationInfo`（`register` 入参）与 `ItemIndex`（`retry` 入参）。
- `OnboardingItem` 与 `ItemIndex` 在类图中存在来自上层的关联（具体父类型未在本视图展开）。
