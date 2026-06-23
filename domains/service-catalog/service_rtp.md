---
id: svc_rtp
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp291
name: rtp
aliases: [gp291_rtp]
related_services: [svc_npss, svc_pns, svc_voucher]
related_tables: []
---

# rtp

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp291` · domain=`service-catalog`。

## 作用
实时支付请求（Request To Pay，调 npss）

## 系统中的位置
- 功能层:即时支付 / 账单 (NPSS / Bill / RTP)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_npss]] npss（即时支付 / 账单） · 2390179 次 · high
- [[svc_pns]] pns（支付通知服务） · 18600 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 13249 次 · high

## 参与的业务场景(cgs 回归)
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）
