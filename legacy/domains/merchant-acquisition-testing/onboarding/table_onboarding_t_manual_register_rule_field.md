---
id: tbl_onboarding_t_manual_register_rule_field
object_type: Table
domain: merchant-acquisition-testing
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags:
- onboarding
- manual-register
- config
subdomain: onboarding
module: manual-register
sensitivity: normal
name: 人工登记字段配置表 t_manual_register_rule_field
aliases:
- t_manual_register_rule_field
related_services: []
related_tables:
- tbl_onboarding_t_manual_register_rule
- tbl_onboarding_t_fund_provider
related_scenarios:
- flow_mpgs_manual_onboarding
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储人工登记规则下每条规则需要录入的字段配置，定义字段名以及该字段是否必填，供 basis 端登记页面与 manualRegister 写入时校验使用。隶属于 onboarding 库，配合 t_manual_register_rule 一起描述某 fund_provider + ruleType 下的人工录入字段集合。

## 关键列
- `id` bigint(20) NOT NULL AUTO_INCREMENT — 主键 id
- `rule_id` bigint(20) NOT NULL — 关联 t_manual_register_rule.id
- `name` varchar(128) NOT NULL — 字段 code/名称
- `mandatory` varchar(20) NOT NULL — 是否必填标识
- `created_time` timestamp(3) NOT NULL — 创建时间

表属性：ENGINE=InnoDB，AUTO_INCREMENT=1，DEFAULT CHARSET=utf8，COMMENT='人工登记字段配置表'。

## 主键/索引
- PRIMARY KEY (`id`)
- UNIQUE KEY `uk_rule_id_name` (`rule_id`,`name`) — 同一规则下字段名唯一

## 校验点(QA 关注)
- `rule_id` 必须存在于 t_manual_register_rule，删除/变更规则时字段配置的一致性
- 同一 `rule_id` 下 `name` 不能重复(uk_rule_id_name)，重复插入应失败
- `mandatory` 取值规范(原文未列举枚举值，需确认有效集合)；为必填的字段在 manualRegister 提交时应被校验非空
- `name` 长度上限 128，超长应被拒绝
- getConfig 接口在 registerType=Manual 时不返回 onboardingRuleList，但人工登记字段配置应通过对应配置接口下发，注意区分
- 字段写入后，manualRegister 将录入数据转换为 item / item_result_map，校验 key 与此处 `name` 的对应关系；同 key 已存在则覆盖
