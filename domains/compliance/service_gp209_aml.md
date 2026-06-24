---
id: svc_aml
object_type: Service
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp209
name: aml
dev_owner: Chao.Li
aliases: [gp209_aml]
related_services: [svc_grc_check_identity_provider, svc_member, svc_remittance, svc_vis, svc_deposit, svc_kyc_service]
related_tables: []
---

# aml

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp209` · domain=`compliance`。

## 作用
反洗钱（AML），调 grc 身份校验

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`compliance`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 20172 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 1496 次 · high
- [[svc_remittance]] remittance（跨境汇款核心） · 522 次 · high
- [[svc_vis]] vis · 12 次 · high
- [[svc_deposit]] deposit（充值 / 存款服务） · 6 次 · high
- [[svc_kyc_service]] kyc-service（实名认证服务） · 4 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant, remittance

## 涉及的 API / 数据库表
**读写的表:** [[tbl_aml_t_system_param]] AML系统参数表 t_system_param

## 参与的业务场景(cgs 回归)
- §7. 跨境汇款（toC，`test_remittance`）

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp209` · domain=`compliance`。
