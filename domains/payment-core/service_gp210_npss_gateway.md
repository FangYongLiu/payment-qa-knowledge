---
id: svc_npss_gateway
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp210
name: npss-gateway
dev_owner: Qian.Wang
aliases: [gp210_npss-gateway]
related_services: [svc_npss]
related_tables: []
---

# npss-gateway

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp210` · domain=`service-catalog`。

## 作用
NPSS（即时支付系统）报文网关

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_npss]] npss（即时支付 / 账单） · 17610 次 · high

**被调用(上游)—— 这些服务调用本服务:**
npss, qpay-npss

## 参与的业务场景(cgs 回归)
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）
