---
id: svc_wechat_channel
object_type: Service
domain: payment-core
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp236
name: wechat-channel
dev_owner: Yadong.Lu
aliases: [gp236_wechat-channel]
related_services: [svc_acs, svc_ues_ws, svc_remittance]
related_tables: []
---

# wechat-channel

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp236` · domain=`service-catalog`。

## 作用
微信支付渠道接入，调 acs 风控 / ues 用户数据

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 2942812 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 736246 次 · med·待核实
- [[svc_remittance]] remittance（跨境汇款核心） · 94 次 · high
