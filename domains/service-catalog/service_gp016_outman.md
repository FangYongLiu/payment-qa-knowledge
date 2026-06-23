---
id: svc_outman
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp016
name: outman
dev_owner: 沈纲领
aliases: [gp016_outman]
related_services: [svc_ufs2, svc_ues_ws, svc_member]
related_tables: []
---

# outman

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp016` · domain=`service-catalog`。

## 作用
outman  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 541426 次 · med·待核实
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 69086 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 4432 次 · high

**被调用(上游)—— 这些服务调用本服务:**
fraud, kyc, member-task
