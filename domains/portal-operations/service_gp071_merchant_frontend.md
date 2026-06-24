---
id: svc_merchant_frontend
object_type: Service
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp071
name: merchant-frontend
dev_owner: Chahid
aliases: [gp071_merchant-frontend]
related_services: [svc_acquireii, svc_merchant, svc_pns, svc_ues_ws, svc_cards, svc_member, svc_fundout, svc_cashdesk_api, svc_statementii]
related_tables: []
---

# merchant-frontend

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp071` · domain=`portal-operations`。

## 作用
SGS 收单网关 / 商户侧支付 BFF —— 商户 acquire 类 API 的入口，转发到 acquireii，并直连 merchant/pns/cards/cashdesk

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`portal-operations`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_acquireii]] acquireii（收单核心） · 23765296 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 15955827 次 · high
- [[svc_pns]] pns（支付通知服务） · 1308283 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 455726 次 · med·待核实
- [[svc_cards]] cards（卡管理） · 364420 次 · high
- [[svc_member]] member（会员 / 账户核心） · 104542 次 · high
- [[svc_fundout]] fundout（出款 / 代付核心） · 79995 次 · high
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 77764 次 · high
- [[svc_statementii]] statementii（账单 / 对账单） · 34589 次 · high

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
