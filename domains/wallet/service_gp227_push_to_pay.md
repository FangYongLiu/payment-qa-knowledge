---
id: svc_push_to_pay
object_type: Service
domain: wallet
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp227
name: push-to-pay
dev_owner: Wujiang.Ding
aliases: [gp227_push-to-pay]
related_services: [svc_member, svc_transfer, svc_csimple]
related_tables: []
---

# push-to-pay

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp227` · domain=`service-catalog`。

## 作用
push-to-pay  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 1682 次 · high
- [[svc_transfer]] transfer · 364 次 · high
- [[svc_csimple]] csimple · 232 次 · high
