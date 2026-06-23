---
id: svc_qpay_zand
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp313
name: qpay-zand
aliases: [gp313_qpay-zand]
related_services: [svc_ues_ws]
related_tables: []
---

# qpay-zand

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp313` · domain=`payment-tools`。

## 作用
Zand 银行渠道接入

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 48 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
reconciliation
