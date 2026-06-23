---
id: svc_mns_listener
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
name: mns-listener
aliases: [gp037_mns-listener]
related_services: [svc_mns_main, svc_ues_ws]
related_tables: []
---

# mns-listener

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp037` · domain=`service-catalog`。

## 作用
消息通知监听（MailNotify/SnsNotify，转 mns-main）

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_mns_main]] mns-main（消息通知中枢） · 3986 次 · med·待核实
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 8 次 · med·待核实
