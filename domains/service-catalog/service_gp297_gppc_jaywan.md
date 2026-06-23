---
id: svc_gppc_jaywan
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp297
name: gppc-jaywan
aliases: [gp297_gppc-jaywan]
related_services: [svc_cms, svc_voucher, svc_tradeii]
related_tables: []
---

# gppc-jaywan

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp297` · domain=`service-catalog`。

## 作用
gppc-jaywan  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cms]] cms（内容 / 配置管理） · 1 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 1 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 1 次 · high
