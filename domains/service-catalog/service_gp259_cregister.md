---
id: svc_cregister
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp259
name: cregister
aliases: [gp259_cregister]
related_services: [svc_router, svc_onboarding]
related_tables: []
---

# cregister

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp259` · domain=`service-catalog`。

## 作用
收款注册 / 收款码服务（推断：下游 router 选渠道）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_router]] router（渠道路由） · 404348 次 · high
- [[svc_onboarding]] onboarding（商户 / 用户入网） · 488 次 · high
