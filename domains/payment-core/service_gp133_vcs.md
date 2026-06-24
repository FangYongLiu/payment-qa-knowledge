---
id: svc_vcs
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp133
name: vcs
dev_owner: Qian.Wang,Giorgi.Kinkladze
aliases: [gp133_vcs]
related_services: [svc_vis]
related_tables: []
---

# vcs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp133` · domain=`payment-core`。

## 作用
vcs  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_vis]] vis · 1081 次 · high
