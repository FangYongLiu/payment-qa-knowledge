---
id: svc_qpay_npss
object_type: Service
domain: acquiring
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp301
name: qpay-npss
aliases: [gp301_qpay-npss]
related_services: [svc_merchant, svc_npss_gateway]
related_tables: []
---

# qpay-npss

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp301` · domain=`acquiring`。

## 作用
支付渠道接入(qpay 适配器)（npss）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`acquiring`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 388 次 · high
- [[svc_npss_gateway]] npss-gateway（NPSS） · 241 次 · high
