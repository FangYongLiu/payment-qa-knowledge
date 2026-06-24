---
id: svc_authorization_service
object_type: Service
domain: payment-core
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp060
name: authorization-service
dev_owner: Yadong.Lu
aliases: [gp060_authorization-service]
related_services: []
related_tables: []
---

# authorization-service

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp060` · domain=`service-catalog`。

## 作用
授权服务（授权 token / 权限，推断）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`service-catalog`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
merchant
