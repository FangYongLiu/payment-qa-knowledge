---
id: svc_contract
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp107
name: contract
aliases: [gp107_contract]
related_services: [svc_ues_ws]
related_tables: []
---

# contract

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp107` · domain=`service-catalog`。

## 作用
contract  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 10 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
ppcenter
