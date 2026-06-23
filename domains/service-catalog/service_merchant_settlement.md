---
id: svc_merchant_settlement
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp288
name: merchant-settlement
aliases: [gp288_merchant-settlement]
related_services: []
related_tables: []
---

# merchant-settlement

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp288` · domain=`service-catalog`。

## 作用
商户结算（被 statementii 调用，推断）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`service-catalog`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
statementii
