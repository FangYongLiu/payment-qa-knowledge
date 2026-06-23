---
id: svc_customer_frontend
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp064
name: customer-frontend
dev_owner: 王斌
aliases: [gp064_customer-frontend]
related_services: [svc_merchant]
related_tables: []
---

# customer-frontend

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp064` · domain=`service-catalog`。

## 作用
C 端用户前端 BFF

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 45 次 · high
