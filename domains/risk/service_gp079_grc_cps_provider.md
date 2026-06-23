---
id: svc_grc_cps_provider
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp079
name: grc-cps-provider
aliases: [gp079_grc-cps-provider]
related_services: [svc_aml]
related_tables: []
---

# grc-cps-provider

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp079` · domain=`risk`。

## 作用
风控合规(GRC)组件（cps-provider）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`risk`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_aml]] aml（反洗钱） · 53 次 · high
