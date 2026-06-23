---
id: svc_botim_snpl
object_type: Service
domain: service-catalog
status: draft
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: callgraph_observed
source_ref: SERVICE_CALLGRAPH_UAT_20260623.md
tags: []
name: botim-snpl
aliases: [botim-snpl]
related_services: [svc_member, svc_pns]
related_tables: []
---

# botim-snpl

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`` · domain=`service-catalog`。

## 作用
botim-snpl  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 16862 次 · med·待核实
- [[svc_pns]] pns（支付通知服务） · 6132 次 · high
