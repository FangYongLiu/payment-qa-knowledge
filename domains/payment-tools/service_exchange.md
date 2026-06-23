---
id: svc_exchange
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp156
name: exchange
aliases: [gp156_exchange]
related_services: []
related_tables: []
---

# exchange

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp156` · domain=`payment-tools`。

## 作用
换汇 / 汇率服务

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-tools`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
cmf, fundout, cmf-task
