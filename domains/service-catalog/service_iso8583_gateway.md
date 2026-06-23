---
id: svc_iso8583_gateway
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp106
name: iso8583-gateway
aliases: [gp106_iso8583-gateway]
related_services: [svc_acs]
related_tables: []
---

# iso8583-gateway

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp106` · domain=`service-catalog`。

## 作用
ISO8583 报文网关（卡组织 / POS 报文接入），调 acs 查 partnerKey

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 580 次 · high
