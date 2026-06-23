---
id: svc_mssii
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp141
name: mssii
dev_owner: 陆亚东
aliases: [gp141_mssii]
related_services: [svc_merchant, svc_member]
related_tables: []
---

# mssii

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp141` · domain=`service-catalog`。

## 作用
营销 / 商户消息服务（推断：调 merchant/member）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 136 次 · high
- [[svc_member]] member（会员 / 账户核心） · 58 次 · high

**被调用(上游)—— 这些服务调用本服务:**
marketing-event
