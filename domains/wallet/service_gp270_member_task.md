---
id: svc_member_task
object_type: Service
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp270
name: member-task
aliases: [gp270_member-task]
related_services: [svc_outman]
related_tables: []
---

# member-task

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp270` · domain=`wallet`。

## 作用
会员 / 账户服务（task）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`wallet`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_outman]] outman · 17346 次 · high
