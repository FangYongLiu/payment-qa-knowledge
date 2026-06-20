---
id: tbl_onboarding_t_manual_register_rule
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
- manual-register
- rule
subdomain: onboarding
module: manual-register
sensitivity: normal
name: 人工登记规则表 t_manual_register_rule
aliases:
- t_manual_register_rule
related_services: []
related_tables:
- tbl_onboarding_t_fund_provider
- tbl_onboarding_t_manual_register_rule_field
related_scenarios:
- mpgs-onboarding-manual-register-design
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储手动报备(人工录入)登记规则，按 `fund_provider_code` + `type`(ruleType) 维度配置。当 `t_fund_provider.register_type=MANUAL` 时，登记类型走人工录入分支，由本表记录该供应商下不同 ruleType 的规则，并通过 `t_manual_register_rule_field` 关联具体字段配置。

## 关键列
- `id` bigint(20) NOT NULL AUTO_INCREMENT — 主键 id
- `type` varchar(50) NOT NULL — ruleType(规则类型，例如商户/门店/设备维度)
- `fund_provider_code` varchar(50) NOT NULL — 资金供应商编码，对应 `t_fund_provider`
- `created_time` timestamp(3) NOT NULL — 创建时间

## 主键/索引
- PRIMARY KEY (`id`)
- UNIQUE KEY `uk_or_type` (`fund_provider_code`,`type`) — 同一供应商同一 ruleType 唯一
- KEY `i_ct` (`created_time`)
- 表参数：ENGINE=InnoDB AUTO_INCREMENT=112 DEFAULT CHARSET=utf8 COMMENT='人工登记规则表'

## 校验点(QA 关注)
- 仅当对应 `t_fund_provider.register_type=MANUAL` 时该规则生效；`registerType=Manual` 时 `getConfig` 返回的 `onboardingRuleList` 为空，需确认人工规则数据从本表读取而非走自动报备规则。
- 唯一键 `uk_or_type`：同一 `fund_provider_code` + `type` 不允许重复插入，重复插入应报唯一键冲突。
- `fund_provider_code` 应与 `t_fund_provider` 中存在的供应商一致(无外键约束，需业务校验)。
- 与 `t_manual_register_rule_field` 通过 `rule_id` 关联，删除/失效规则时需关注字段级联一致性。
- 字段均 NOT NULL，缺失 `type`/`fund_provider_code`/`created_time` 应写入失败。
