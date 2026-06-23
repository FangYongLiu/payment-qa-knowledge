---
id: svc_merchant_console_frontend
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp045
name: merchant-console-frontend
dev_owner: 王斌
aliases: [gp045_merchant-console-frontend]
related_services: [svc_member, svc_merchant, svc_grc_check_identity_provider]
related_tables: []
---

# merchant-console-frontend

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp045` · domain=`service-catalog`。

## 作用
商户控制台前端 BFF（商户后台操作入口）

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_member]] member（会员 / 账户核心） · 27 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 9 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 3 次 · med·待核实
