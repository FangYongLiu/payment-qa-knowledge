---
id: svc_cmf_task
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp002
name: cmf-task
aliases: [gp002_cmf-task]
related_services: [svc_router, svc_exchange, svc_ues_ws, svc_cashdesk_api, svc_grc_check_identity_provider, svc_member]
related_tables: []
---

# cmf-task

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp002` · domain=`payment-tools`。

## 作用
cmf 异步任务（定时 / 后台渠道处理）

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_router]] router（渠道路由） · 1727860 次 · high
- [[svc_exchange]] exchange（换汇 / 汇率服务） · 1206 次 · med·待核实
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 550 次 · med·待核实
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 186 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 25 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 2 次 · high
