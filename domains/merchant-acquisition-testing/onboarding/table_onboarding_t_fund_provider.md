---
id: tbl_onboarding_t_fund_provider
object_type: Table
domain: merchant-acquisition-testing
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7c033704-1056-4e5a-9598-3d67ba9edba4
tags:
- onboarding
- fund_provider
subdomain: onboarding
module: null
sensitivity: normal
name: 资金供应商配置表 t_fund_provider
aliases: []
related_services: []
related_tables:
- tbl_onboarding_t_manual_register_rule
- tbl_onboarding_t_manual_register_rule_field
related_scenarios:
- mpgs-onboarding-manual-register-design
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
资金供应商(FundProvider)配置表，归属 `onboarding` 库。本次为支持 MPGS Onboarding 手动报备能力，在表中新增 `register_type` 字段，用以标识该供应商的登记类型(系统自动 / 人工录入)，从而区分自动报备与手动报备两种流转链路。

## 关键列
- `register_type` varchar(50) NOT NULL DEFAULT `'SYSTEM_AUTO'`
  - 含义：报备类型
  - 取值：`SYSTEM_AUTO`、`MANUAL`
  - 用途：getConfig 接口返回的 `registerType` 即来源于此字段；当 `registerType=Manual` 时，`onboardingRuleList` 返回为空，由 t_manual_register_rule / t_manual_register_rule_field 提供人工登记字段配置。

## 主键/索引
原文未列出 t_fund_provider 表的主键与索引定义(仅给出 ALTER 新增列语句)。

DDL 变更：
```sql
ALTER TABLE `onboarding`.`t_fund_provider`
ADD COLUMN `register_type` varchar(50) NOT NULL DEFAULT 'SYSTEM_AUTO'
COMMENT '报备类型，SYSTEM_AUTO、MANUAL';
```

## 校验点(QA 关注)
- 新增 `register_type` 列默认值校验：存量数据 ALTER 后应全部为 `SYSTEM_AUTO`，不影响既有自动报备流程。
- 取值约束：仅允许 `SYSTEM_AUTO` 或 `MANUAL`，非法值需在配置入口拦截。
- 与 getConfig 接口联动：
  - `register_type=SYSTEM_AUTO` 时，返回的 `onboardingRuleList` 应为原自动报备规则。
  - `register_type=MANUAL` 时，返回的 `onboardingRuleList` 应为空，人工登记字段从 t_manual_register_rule / t_manual_register_rule_field 获取。
- 配置切换：在 basis 页面切换登记类型后，t_fund_provider 中的 `register_type` 应同步更新，且不影响已存在的 onboarding 数据。
- 兼容性：未配置或老数据缺省时，按 `SYSTEM_AUTO` 走自动报备链路。
