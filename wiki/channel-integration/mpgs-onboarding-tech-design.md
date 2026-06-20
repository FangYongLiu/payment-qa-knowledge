---
title: MPGS Onboarding技术方案
domain: channel-integration
kind: wiki_page
slug: mpgs-onboarding-tech-design
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:fdd8444b-c0ce-48af-8f1d-db846d5b0da8
tags: []
---

# MPGS Onboarding技术方案

本页描述 MPGS 渠道入驻（Onboarding）的核心数据模型与 Facade 接口设计，用于支撑入驻信息注册、查询与失败重试。

## 数据模型

### OnboardingItem
表示一笔入驻条目的完整信息。

- `fundProviderCode: string`
- `ownerId: string`
- `resultParamMap: map<string,string>`
- `status: OnboardingItemStatus`
- `type: ItemType`

### ItemIndex
作为 OnboardingItem 的查询键（lookup key），由三元组定位条目。

- `fundProviderCode: string`
- `ownerId: string`
- `type: ItemType`

### ItemRegistrationInfo
入驻注册时携带的注册信息集合，按 ItemType 维度组织参数。

- `fundProviderCode: string`
- `ownerId: string`
- `registrationInfoMap: map<ItemType, Map<string,string>>`

## Facade接口

### OnboardingItemFacade
负责入驻条目的查询。

- `getItem(ItemIndex): OnboardingItem` —— 根据 ItemIndex 返回对应的 OnboardingItem。

### OnboardingFacade
负责入驻注册与重试。

- `registerItem(ItemRegistrationInfo): boolean` —— 提交注册信息，触发入驻。
- `retry(ItemIndex): void` —— 针对指定 ItemIndex 的入驻条目进行重试。

## 关系说明

- `OnboardingItemFacade` 依赖 `ItemIndex`（入参）并返回 `OnboardingItem`。
- `OnboardingFacade` 依赖 `ItemRegistrationInfo`（`registerItem` 入参）与 `ItemIndex`（`retry` 入参）。
- `ItemIndex` 由 `fundProviderCode + ownerId + type` 唯一标识一笔入驻条目，用于查询与重试场景的定位。
