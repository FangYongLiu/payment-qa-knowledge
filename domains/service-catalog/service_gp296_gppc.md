---
id: svc_gppc
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp296
name: gppc
aliases: [gp296_gppc]
related_services: [svc_grc_check_identity_provider]
related_tables: []
---

# gppc

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp296` · domain=`service-catalog`。

## 作用
gppc  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 2 次 · med·待核实
