---
id: svc_fraud
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp192
name: fraud
dev_owner: 沈纲领
aliases: [gp192_fraud]
related_services: [svc_member, svc_outman]
related_tables: []
---

# fraud

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp192` · domain=`risk`。

## 作用
fraud  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`risk`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 1458 次 · high
- [[svc_outman]] outman · 729 次 · high
