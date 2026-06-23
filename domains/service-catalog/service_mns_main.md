---
id: svc_mns_main
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
name: mns-main
aliases: [gp037_mns-main]
related_services: [svc_ues_ws]
related_tables: []
---

# mns-main

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp037` · domain=`service-catalog`。

## 作用
消息通知中枢（短信 / 邮件 / 推送，被 mns-listener 调用）

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 1004 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
mns-listener, cashierii
