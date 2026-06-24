---
id: svc_qpay_nipos
object_type: Service
domain: acquiring
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp244
name: qpay-nipos
aliases: [gp244_qpay-nipos]
related_services: [svc_cmf]
related_tables: []
---

# qpay-nipos

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp244` · domain=`acquiring`。

## 作用
NI POS 渠道接入

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`acquiring`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cmf]] cmf（渠道管理与资金） · 36425 次 · high
