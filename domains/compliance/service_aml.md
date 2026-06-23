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
dev_owner: 许广
aliases: [gp209_aml]
related_services: [svc_grc_check_identity_provider]
related_tables: []
---

# aml

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp209` · domain=`compliance`。

## 作用
反洗钱（AML），调 grc 身份校验

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`compliance`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 141 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
merchant, remittance

## 参与的业务场景(cgs 回归)
- §7. 跨境汇款（toC，`test_remittance`）
