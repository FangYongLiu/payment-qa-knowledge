---
id: svc_mns_scheduler
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp037
name: mns-scheduler
aliases: [gp037_mns-scheduler]
related_services: [svc_ues_ws]
related_tables: []
---

# mns-scheduler

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp037` · domain=`service-catalog`。

## 作用
消息通知调度（定时通知，调 ues）

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 12 次 · med·待核实
