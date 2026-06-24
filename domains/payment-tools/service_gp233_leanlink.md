---
id: svc_leanlink
object_type: Service
domain: payment-tools
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp233
name: leanlink
dev_owner: Guoyou.Ma
aliases: [gp233_leanlink]
related_services: [svc_vis, svc_member]
related_tables: []
---

# leanlink

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp233` · domain=`service-catalog`。

## 作用
leanlink  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_vis]] vis · 52 次 · high
- [[svc_member]] member（会员 / 账户核心） · 32 次 · high

**被调用(上游)—— 这些服务调用本服务:**
qpay-lean
