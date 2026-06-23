---
id: svc_qpay_nipos
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp244
name: qpay-nipos
aliases: [gp244_qpay-nipos]
related_services: [svc_cmf]
related_tables: []
---

# qpay-nipos

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp244` · domain=`payment-tools`。

## 作用
NI POS 渠道接入

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_cmf]] cmf（渠道管理与资金） · 22 次 · high
