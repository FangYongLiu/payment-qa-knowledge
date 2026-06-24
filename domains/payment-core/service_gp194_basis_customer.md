---
id: svc_basis_customer
object_type: Service
domain: payment-core
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp194
name: basis-customer
dev_owner: Yibing.Xia
aliases: [gp194_basis-customer]
related_services: [svc_ufs2, svc_member]
related_tables: []
---

# basis-customer

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp194` · domain=`service-catalog`。

## 作用
基础数据(Basis)（customer）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 273 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 70 次 · high
