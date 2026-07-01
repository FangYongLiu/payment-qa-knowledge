---
id: api_onboarding_get_config
object_type: API
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags:
- onboarding
- fund-provider
- config
subdomain: onboarding
module: fund-provider-config
sensitivity: normal
name: 供应商登记配置查询接口 getConfig
aliases: []
related_services:
- svc_onboarding
---

## 用途
查询供应商登记配置，返回 registerType 标识该供应商的登记类型(系统自动 SYSTEM_AUTO 或人工录入 MANUAL)，供上游(basis 服务/前端)判断是走自动报备还是人工录入流程。

## 路径/方法
原文未给出具体 HTTP 路径与方法，仅以 `getConfig` 接口名标识(归属 onboarding 服务的 fund-provider 配置 API)。

## 入参
原文未列出入参字段(仅在接口图 onboarding-fund-provider-config-api.bmp 中体现)。

## 出参
- `registerType`：供应商登记类型标识
  - `SYSTEM_AUTO`：系统自动报备
  - `MANUAL`：人工录入登记
- `onboardingRuleList`：登记规则列表
  - 当 `registerType = MANUAL` 时，`onboardingRuleList` 为空
  - 当 `registerType = SYSTEM_AUTO` 时，返回原有自动报备规则

## 错误码
原文未明确列出。

## 测试校验点
- 供应商 `register_type=SYSTEM_AUTO` 时，`registerType` 返回 `SYSTEM_AUTO`，且 `onboardingRuleList` 按既有自动报备规则正常返回，不为空。
- 供应商 `register_type=MANUAL` 时，`registerType` 返回 `MANUAL`，且 `onboardingRuleList` 必须为空(不返回自动报备规则)。
- `t_fund_provider.register_type` 字段默认值为 `SYSTEM_AUTO`，未显式设置时接口应返回 `SYSTEM_AUTO`。
- `register_type` 仅允许 `SYSTEM_AUTO`、`MANUAL` 两种取值，其他取值的容错/异常表现需校验。
- 切换登记类型(自动 ↔ 人工)后，再次调用 getConfig 应实时反映最新 `registerType` 与对应的规则列表内容。
- 与下游联动：basis 服务/前端依据 `registerType` 渲染自动报备页或人工录入弹窗，需校验 MANUAL 时不会因 `onboardingRuleList` 为空导致异常。
