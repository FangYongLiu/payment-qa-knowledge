---
id: scn_mpgs_onboarding
object_type: Scenario
name: MPGS Onboarding 组件架构与数据模型
aliases: [MPGS入网, MPGS onboarding]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:c2d176f8-25d1-4750-bf00-2a53a12f317a; wiki_image:fdd8444b-c0ce-48af-8f1d-db846d5b0da8
tags: [mpgs, onboarding, 入网, 组件架构]
related_services: [svc_qpay_mpgs]
related_tables: []
related_logs: []
---

# MPGS Onboarding 组件架构与数据模型

## 触发 / 入口
MPGS 渠道入驻(Onboarding)的组件依赖关系与核心数据模型 / Facade 接口设计,用于支撑入驻信息注册、查询与失败重试的测试与排障。

## 关联关系
- **涉及服务**:[[svc_qpay_mpgs]];basis、onboarding、ppcenter、cmf、qpay-ni(后四者服务对象待补)

## 组件依赖关系
- `basis` → `onboarding`
- `onboarding` → `ppcenter`
- `onboarding` ↔ `cmf`(双向依赖)
- `cmf` → `qpay-ni`
- `qpay-ni` → `onboarding`(回调,形成 `onboarding → cmf → qpay-ni → onboarding` 闭环)
拓扑:basis 顶层 → onboarding(核心节点,向右调 ppcenter,与 cmf 双向)→ cmf → qpay-ni(底层,经左侧回路回调 onboarding)。

## 数据模型
### OnboardingItem(一笔入驻条目)
- `fundProviderCode: string`、`ownerId: string`、`resultParamMap: map<string,string>`、`status: OnboardingItemStatus`、`type: ItemType`。

### ItemIndex(查询键)
- `fundProviderCode + ownerId + type` 三元组唯一定位条目。

### ItemRegistrationInfo(注册信息)
- `fundProviderCode`、`ownerId`、`registrationInfoMap: map<ItemType, Map<string,string>>`。

## Facade 接口
- `OnboardingItemFacade.getItem(ItemIndex): OnboardingItem` —— 按 ItemIndex 查条目。
- `OnboardingFacade.registerItem(ItemRegistrationInfo): boolean` —— 提交注册触发入驻。
- `OnboardingFacade.retry(ItemIndex): void` —— 对指定条目重试入驻。

## DB / 校验点
- 入驻注册后 OnboardingItem 的 status 流转;失败条目 retry 是否按 ItemIndex 正确定位。
- 待补:具体落库表、status 枚举值原文未提供。

## 预期结果
- registerItem 成功创建/更新 OnboardingItem;getItem 按三元组返回正确条目;retry 可对失败条目重试。
