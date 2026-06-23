---
id: svc_npss
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp222
name: npss
dev_owner: 王迁
aliases: [gp222_npss]
related_services: [svc_member]
related_tables: []
---

# npss

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp222` · domain=`service-catalog`。

## 作用
即时支付 / 账单（NPSS，被 rtp 调用）

## 系统中的位置
- 功能层:即时支付 / 账单 (NPSS / Bill / RTP)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_member]] member（会员 / 账户核心） · 21 次 · high

**被调用(上游)—— 这些服务调用本服务:**
rtp, npss-gateway

## 参与的业务场景(cgs 回归)
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）
