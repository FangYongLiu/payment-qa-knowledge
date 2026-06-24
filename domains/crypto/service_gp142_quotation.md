---
id: svc_quotation
object_type: Service
domain: crypto
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp142
name: quotation
dev_owner: Sijia.Zhang
aliases: [gp142_quotation]
related_services: [svc_asset_info]
related_tables: []
---

# quotation

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp142` · domain=`crypto`。

## 作用
报价服务（加密货币 / 汇率，调 asset-info、Binance 行情）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`crypto`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_asset_info]] asset-info（资产信息） · 60921 次 · high

**被调用(上游)—— 这些服务调用本服务:**
holding
