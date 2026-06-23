---
id: svc_remittance_bdo
object_type: Service
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp264
name: remittance-bdo
aliases: [gp264_remittance-bdo]
related_services: [svc_ues_ws]
related_tables: []
---

# remittance-bdo

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp264` · domain=`remittance`。

## 作用
跨境汇款渠道接入（bdo）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`remittance`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 5323349 次 · med·待核实
