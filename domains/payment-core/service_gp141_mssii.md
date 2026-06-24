---
id: svc_mssii
object_type: Service
domain: payment-core
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp141
name: mssii
dev_owner: Yadong.Lu
aliases: [gp141_mssii]
related_services: [svc_merchant, svc_member, svc_kyc]
related_tables: []
---

# mssii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp141` · domain=`service-catalog`。

## 作用
营销 / 商户消息服务（推断：调 merchant/member）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 4366 次 · high
- [[svc_member]] member（会员 / 账户核心） · 2918 次 · high
- [[svc_kyc]] kyc（实名认证） · 1598 次 · high

**被调用(上游)—— 这些服务调用本服务:**
marketing-event
