---
id: svc_grc_check_identity_provider
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp079
name: grc-check-identity-provider
dev_owner: 李德文
aliases: [gp079_grc-check-identity-provider]
related_services: [svc_member]
related_tables: []
---

# grc-check-identity-provider

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp079` · domain=`risk`。

## 作用
风控合规身份校验（GRC）—— 被 cashier/cashdesk/cmf/aml 调用做风险事件 / 身份校验

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`risk`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_member]] member（会员 / 账户核心） · 162 次 · high

**被调用(上游)—— 这些服务调用本服务:**
cashierii, cashdesk-api, cmf, aml, qpay-mpgs, remittance
