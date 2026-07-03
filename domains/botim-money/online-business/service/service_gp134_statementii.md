---
id: svc_statementii
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp134
name: statementii
dev_owner: Shuo.Wang
aliases: [gp134_statementii]
related_services: [svc_merchant_settlement]
related_tables:
- tbl_statementii_t_retry_task
- tbl_statementii_t_sequence_table
- tbl_statementii_t_settlement_config
- tbl_statementii_t_settlement_config_bak
- tbl_statementii_t_settlement_order
- tbl_statementii_t_statement_balance
- tbl_statementii_t_statement_config
- tbl_statementii_t_statement_period
- tbl_statementii_t_statement_rebate
- tbl_statementii_t_statement_report
- tbl_statementii_t_statement_settlement
- tbl_statementii_t_statement_subscribe
- tbl_statementii_t_statement_task
- tbl_statementii_t_statement_task_lock
- tbl_statementii_t_statement_transaction
- tbl_statementii_t_template_version_change_log
---

# statementii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp134` · domain=`online-business`。

## 作用
账单 / 对账单（Statement II），调 fund-charge-query/settlement/withdraw

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`online-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_merchant_settlement]] merchant-settlement（商户结算） · 129142 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_merchant_onboarding]](流程:商户注册与入驻端到端流程(Acquire + WPS))
- [[scn_merchant_settlement_withdraw_auth]](场景:商户控台结算/提现/退款的双人授权)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp134` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `statementii` 库(16 张,见 `online-business/table/statementii/`)。主要表:[[tbl_statementii_t_settlement_config]] · [[tbl_statementii_t_settlement_config_bak]] · [[tbl_statementii_t_settlement_order]] · [[tbl_statementii_t_statement_settlement]] · [[tbl_statementii_t_statement_transaction]]。
