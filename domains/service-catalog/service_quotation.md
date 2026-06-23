---
id: svc_quotation
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp142
name: quotation
dev_owner: 刘舟
aliases: [gp142_quotation]
related_services: [svc_asset_info]
related_tables: []
---

# quotation

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp142` · domain=`service-catalog`。

## 作用
报价服务（加密货币 / 汇率，调 asset-info、Binance 行情）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_asset_info]] asset-info（资产信息） · 468 次 · high
