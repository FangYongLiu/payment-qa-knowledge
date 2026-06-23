---
id: tbl_onboarding_t_manual_register_rule
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags:
- onboarding
- manual-register
- mysql
subdomain: onboarding
module: manual-register
sensitivity: normal
name: 人工登记规则表 t_manual_register_rule
aliases:
- t_manual_register_rule
related_services:
- svc_onboarding
---

## 用途
存储手动报备(MANUAL)模式下的登记规则，按 `fund_provider_code` + `type` 维度唯一定义一条规则，用于驱动 basis 侧人工录入页面的字段配置(配合 `t_manual_register_rule_field` 使用)。

仅当 `t_fund_provider.register_type = 'MANUAL'` 时使用本表配置；此时 `getConfig` 接口返回的 `onboardingRuleList` 为空，登记规则改由本表(及 field 子表)提供。

## 关键列
- `id` bigint(20) NOT NULL AUTO_INCREMENT — 主键 id
- `type` varchar(50) NOT NULL — ruleType，登记规则类型(如商户、门店、设备等维度)
- `fund_provider_code` varchar(50) NOT NULL — 资金供应商编码，关联 `t_fund_provider`
- `created_time` timestamp(3) NOT NULL — 创建时间

表注释：`人工登记规则表`；ENGINE=InnoDB；DEFAULT CHARSET=utf8；AUTO_INCREMENT=112。

## 主键/索引
- PRIMARY KEY (`id`)
- UNIQUE KEY `uk_or_type` (`fund_provider_code`, `type`) — 同一供应商下同一 ruleType 唯一
- KEY `i_ct` (`created_time`)

## 校验点(QA 关注)
- 唯一约束：同一 `fund_provider_code` + `type` 组合不可重复插入，违反应被 `uk_or_type` 拦截。
- `type`、`fund_provider_code`、`created_time` 均为 NOT NULL，缺失应报错。
- 与 `t_fund_provider.register_type` 联动：仅 MANUAL 类型供应商才应配置本表规则；SYSTEM_AUTO 不应使用本表。
- 与子表 `t_manual_register_rule_field` 关联：通过 `rule_id` 关联，校验规则删除/变更时字段配置一致性。
- `getConfig` 在 `registerType=Manual` 时 `onboardingRuleList` 应为空，规则数据来源切换为本表，需校验前端取数路径正确。
- 字段长度边界：`type` ≤50、`fund_provider_code` ≤50。
