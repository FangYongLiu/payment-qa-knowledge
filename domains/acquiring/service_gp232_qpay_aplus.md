---
id: svc_qpay_aplus
object_type: Service
domain: acquiring
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp232
name: qpay-aplus
dev_owner: Hefei.Zhang
aliases: [gp232_qpay-aplus]
related_services: [svc_merchant]
related_tables: []
---

# qpay-aplus

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp232` · domain=`acquiring`。

## 作用
支付渠道接入(qpay 适配器)（aplus）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`acquiring`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 62 次 · high
