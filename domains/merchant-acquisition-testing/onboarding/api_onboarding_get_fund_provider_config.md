---
id: api_onboarding_get_fund_provider_config
object_type: API
domain: merchant-acquisition-testing
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7c033704-1056-4e5a-9598-3d67ba9edba4
tags:
- onboarding
- fund-provider
- config
subdomain: onboarding
module: fund-provider
sensitivity: normal
name: FundProvider配置查询接口 getConfig
aliases: []
related_services: []
related_tables:
- tbl_onboarding_t_fund_provider
- tbl_onboarding_t_manual_register_rule
- tbl_onboarding_t_manual_register_rule_field
related_scenarios:
- mpgs-onboarding-manual-register-design
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
查询 FundProvider 配置信息，返回供应商登记类型 registerType，用于区分自动报备(SYSTEM_AUTO)与人工录入(MANUAL)两种登记模式，供调用方决定后续报备流程走向。

## 路径/方法
原文未给出具体路径与 HTTP 方法，仅在 onboarding-fund-provider-config-api 中标识为 getConfig 接口。

## 入参
原文未列出入参字段。

## 出参
- registerType：供应商登记类型标识
  - SYSTEM_AUTO：系统自动报备
  - MANUAL：人工录入报备
- onboardingRuleList：自动报备规则列表
  - 当 registerType 为 MANUAL 时，onboardingRuleList 为空

## 错误码
原文未列出。

## 测试校验点
- 当 t_fund_provider.register_type = SYSTEM_AUTO 时，接口返回 registerType=SYSTEM_AUTO，且 onboardingRuleList 正常返回自动报备规则
- 当 t_fund_provider.register_type = MANUAL 时，接口返回 registerType=MANUAL，且 onboardingRuleList 为空
- t_fund_provider.register_type 默认值为 SYSTEM_AUTO，未配置时接口返回应等同于自动报备
- registerType 字段值仅支持 SYSTEM_AUTO、MANUAL 两类枚举
