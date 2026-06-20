---
id: tbl_onboarding_t_manual_register_rule_field
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
- mysql
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
- mpgs-onboarding-manual-register-design
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储人工登记规则下的字段配置，记录每条规则(t_manual_register_rule)所需录入的字段名称及是否必填，供 basis 页面渲染人工录入弹窗与提交时校验使用。所属库：`onboarding`。

## 关键列
- `id` bigint(20) NOT NULL AUTO_INCREMENT — 主键 id
- `rule_id` bigint(20) NOT NULL — 关联 t_manual_register_rule.id
- `name` varchar(128) NOT NULL — 字段名(code)
- `mandatory` varchar(20) NOT NULL — 是否必填
- `created_time` timestamp(3) NOT NULL — 创建时间

表属性：ENGINE=InnoDB, AUTO_INCREMENT=1, DEFAULT CHARSET=utf8, COMMENT='人工登记字段配置表'。

## 主键/索引
- PRIMARY KEY (`id`)
- UNIQUE KEY `uk_rule_id_name` (`rule_id`,`name`) — 同一 rule 下字段名唯一

## 校验点(QA 关注)
- `rule_id` + `name` 唯一性：同一规则下不允许重复字段名，重复插入应受 `uk_rule_id_name` 约束拒绝。
- `name`/`mandatory` 均为 NOT NULL，建表未给默认值，写入时必须显式赋值。
- `mandatory` 为 varchar(20)，需确认应用层取值集合(必填/非必填)是否标准化，避免脏值。
- `rule_id` 与 t_manual_register_rule.id 的引用一致性：rule 删除/变更时，字段配置是否同步处理(库级未定义外键)。
- 字段配置驱动 manualRegister 接口录入项与必填校验，需校验前端弹窗渲染、后端提交校验与本表配置一致。
- 仅在 t_fund_provider.register_type = 'MANUAL' 的供应商规则下使用，自动报备规则不应产生本表数据。
