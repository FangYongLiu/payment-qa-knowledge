---
id: svc_feebill
object_type: Service
domain: payment-core
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp239
name: feebill
dev_owner: Yongxing.Cao
aliases: [gp239_feebill]
related_services: [svc_pns]
related_tables: []
---

# feebill

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp239` · domain=`service-catalog`。

## 作用
feebill  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_pns]] pns（支付通知服务） · 6 次 · high
