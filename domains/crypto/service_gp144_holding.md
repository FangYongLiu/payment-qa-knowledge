---
id: svc_holding
object_type: Service
domain: crypto
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp144
name: holding
dev_owner: Sijia.Zhang
aliases: [gp144_holding]
related_services: [svc_quotation, svc_member, svc_asset_info]
related_tables: []
---

# holding

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp144` · domain=`crypto`。

## 作用
holding  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`crypto`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_quotation]] quotation（报价服务） · 5448 次 · high
- [[svc_member]] member（会员 / 账户核心） · 2652 次 · high
- [[svc_asset_info]] asset-info（资产信息） · 2379 次 · high

**被调用(上游)—— 这些服务调用本服务:**
member-front
