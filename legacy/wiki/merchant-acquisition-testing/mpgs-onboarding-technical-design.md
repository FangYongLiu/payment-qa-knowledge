---
title: MPGS Onboarding技术方案设计
domain: merchant-acquisition-testing
kind: wiki_page
slug: mpgs-onboarding-technical-design
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:154b7f29-4373-456c-81b9-4adfc45d4300
tags: []
---

# MPGS Onboarding技术方案设计

本页给出 MPGS 渠道商户入驻的核心领域模型与 Facade 接口设计，覆盖入驻项的数据结构、查询索引、注册信息以及读写两类外观接口。

## 领域模型

### OnboardingItem
表示一笔入驻项的当前状态与结果。

- `fundProviderCode: string`
- `ownerId: string`
- `resultParamMap: map<string,string>`
- `status: OnboardingItemStatus`
- `type: ItemType`

### ItemIndex
用于唯一定位一笔 OnboardingItem 的索引键。

- `fundProviderCode: string`
- `ownerId: string`
- `type: ItemType`

### ItemRegistrationInfo
用于发起注册时携带的入参信息，按 `ItemType` 维度组织。

- `fundProviderCode: string`
- `ownerId: string`
- `registrationInfoMap: map<ItemType, Map<string,string>>`

## Facade 接口

设计上拆分为读、写两个 Facade。

### OnboardingItemFacade（读）
- `getItem(ItemIndex): OnboardingItem` — 按索引查询入驻项。

### OnboardingFacade（写）
> 类图中拼写为 `OnbaordingFacade`，疑似笔误。

- `register(ItemRegistrationInfo): boolean` — 发起入驻注册。
- `retry(ItemIndex): void` — 对指定入驻项发起重试。

## 关系说明

- `OnboardingItemFacade` 依赖 `ItemIndex`（入参）与 `OnboardingItem`（返回值）。
- `OnboardingFacade` 依赖 `ItemRegistrationInfo`（`register` 入参）与 `ItemIndex`（`retry` 入参）。
- `OnboardingItem` 与 `ItemIndex` 共享 `fundProviderCode`、`ownerId`、`type` 三元组作为业务键。
