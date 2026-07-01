---
id: flow_mpgs_manual_onboarding
object_type: Flow
name: MPGS 手动报备(人工录入)入驻流程
aliases: [MPGS manual onboarding, 手动报备, manual register onboarding]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags: [onboarding, mpgs, manual-register]
related_services: [svc_basis, svc_onboarding]
related_tables: [tbl_onboarding_t_fund_provider, tbl_onboarding_t_manual_register_rule, tbl_onboarding_t_manual_register_rule_field]
related_scenarios: [scn_onboarding_manual_register]
---

# MPGS 手动报备(人工录入)入驻流程

## 概述
为支持 MPGS E-com 快速上线、规避 Visa 对 Game merchant 的封禁风险,在现有 Onboarding 体系内新增「人工录入」报备通路:商户先在外部 **MPGS Onboarding Portal** 线下完成登记,再把结果同步回 Payby 系统。起点 = 运营在 basis 门户配置供应商登记类型并发起人工录入;终点 = 登记 item 与 item_result_map 写入并置为「激活」。

> 与系统自动报备(`SYSTEM_AUTO`)互斥:自动报备走 OnboardingOrder 状态流转;人工报备(`MANUAL`)采用轻量「仅写入报备结果」方案(方案三),不维护 OnboardingOrder。

## 步骤(跨系统)
1. [[svc_basis]](basis 门户)— 运营在 FundProvider 配置页选择「登记类型」:`SYSTEM_AUTO`(系统自动) / `MANUAL`(人工录入)。登记类型落在 [[tbl_onboarding_t_fund_provider]] 的 `register_type` 字段。
2. [[svc_basis]] → [[svc_onboarding]] — 前端调配置查询接口 [[api_onboarding_get_config]];当 `registerType = Manual` 时返回 `onboardingRuleList` 为空,改用人工登记规则(来自 [[tbl_onboarding_t_manual_register_rule]] / [[tbl_onboarding_t_manual_register_rule_field]])渲染人工录入弹窗。
3. 线下:商户在 MPGS Onboarding Portal 完成商户 / 门店 / 设备(MERCHANT / STORE / DEVICE 三层)的登记。
4. [[svc_basis]](人工录入弹窗)→ [[svc_onboarding]] — 运营在 basis 登记页以人工录入方式提交报备信息,调用写入接口 [[api_onboarding_manual_register]]。
5. [[svc_onboarding]] — 接口内部把录入数据转换为登记 item 与 item_result_map 并置为「激活」;同 key 已存在则覆盖;写入失败抛错由上游重试。不创建/维护 OnboardingOrder。

## 关联关系
- **经过的服务(有序)**:[[svc_basis]](门户配置 + 人工录入弹窗)→ [[svc_onboarding]](配置查询 + 报备结果写入)(= `related_services`)
- **关键表**:[[tbl_onboarding_t_fund_provider]](`register_type` 区分自动/手动)、[[tbl_onboarding_t_manual_register_rule]] / [[tbl_onboarding_t_manual_register_rule_field]](人工登记规则与字段)(= `related_tables`)
- **关键场景**:[[scn_onboarding_manual_register]](= `related_scenarios`)
- **涉及接口**:[[api_onboarding_get_config]](返回 `registerType`)、[[api_onboarding_manual_register]](写入报备结果)

## 领域模型(技术方案背景)
人工/自动报备共用一套领域模型(来自 MPGS Onboarding 类图,UML 设计):

- `ItemType` 枚举:`MERCHANT` / `STORE` / `DEVICE`(入驻对象三层级)。
- `RegisterItem`(基类):`fundProviderCode` / `ownerId` / `resultParamMap` / `type`。
- `OnboardingItem`:继承 `RegisterItem`,额外带 `status: OnboardingItemStatus`(具体取值原文未列,待补)。
- `ManualRegisterItem`:继承 `RegisterItem`(类图未列额外字段)。
- `ItemIndex`:业务键三元组 `fundProviderCode` + `ownerId` + `type`,用于唯一定位一笔 item。
- `ItemRegistrationInfo`:发起注册的入参,`registrationInfoMap: map<ItemType, map<string,string>>`。
- Facade(读写分离):
  - `OnboardingItemFacade.getItem(ItemIndex): OnboardingItem`(读)。
  - `OnboardingFacade.register(ItemRegistrationInfo): boolean`、`OnboardingFacade.retry(ItemIndex): void`、`manualRegister(ManualRegisterItem): boolean`(写)。
  - 注:类图中拼写为 `OnbaordingFacade`,疑似笔误。

## 方案选型(为什么用方案三)
| 方案 | 实现 | 是否采用 |
|---|---|---|
| 一:复用自动报备流转逻辑 | 自动/手动逻辑耦合,状态流转可能不一致 | 不考虑 |
| 二:OnboardingOrder 新增上报方式属性 | 隔离自动/手动,扩展互不影响 | 备选 |
| 三:仅写入报备结果信息 | 直接写 item + item_result_param 并激活,失败抛错由上游重试;轻量、对自动上报无影响;缺点是不维护 OnboardingOrder,无法查看登记记录(OnboardingOrder 未对外暴露) | **采用** |

选型结论:人工上报场景中商户已在外部供应商处完成注册,回传只是把信息同步回 Payby,故采用方案三。

## 数据库变更
- [[tbl_onboarding_t_fund_provider]] 增加 `register_type` 字段:
  ```sql
  ALTER TABLE `onboarding`.`t_fund_provider`
  ADD COLUMN `register_type` varchar(50) NOT NULL DEFAULT 'SYSTEM_AUTO'
  COMMENT '报备类型，SYSTEM_AUTO、MANUAL';
  ```
- 新增人工登记规则表 [[tbl_onboarding_t_manual_register_rule]]。
- 新增人工登记字段配置表 [[tbl_onboarding_t_manual_register_rule_field]]。

## 校验点
- `register_type = MANUAL` 的供应商,[[api_onboarding_get_config]] 返回 `registerType=Manual` 且 `onboardingRuleList` 为空,改走人工登记规则字段。
- 人工录入提交后,登记 item 与 item_result_map 写入且状态为「激活」;同 key 覆盖;不产生 OnboardingOrder。
- 自动报备(`SYSTEM_AUTO`)流程不受影响,二者隔离。
- 写入失败应抛错以便上游重试。
