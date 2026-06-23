---
id: svc_statementii
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp134
name: statementii
aliases: [gp134_statementii]
related_services: [svc_merchant_settlement]
related_tables: []
---

# statementii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp134` · domain=`service-catalog`。

## 作用
账单 / 对账单（Statement II），调 fund-charge-query/settlement/withdraw

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_merchant_settlement]] merchant-settlement（商户结算） · 129142 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend
