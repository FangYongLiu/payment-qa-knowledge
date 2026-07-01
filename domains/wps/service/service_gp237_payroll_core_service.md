---
id: svc_payroll_core_service
object_type: Service
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp237
name: payroll-core-service
dev_owner: Youwei.Bi
aliases: [gp237_payroll-core-service]
related_services: []
related_tables: []
---

# payroll-core-service

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp237` · domain=`wps`。

## 作用
(本窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`wps`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 参与的业务场景(cgs 回归)
- §11. WPS 代发工资（`wps/wps_test.py`）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_wps_company_onboarding_to_payroll]](流程:WPS 企业入驻到发薪端到端流程)
- [[scn_wps_sif_vs_paf]](场景:WPS SIF 与 PAF 公司类型差异化发薪)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp237` · domain=`wps`。
