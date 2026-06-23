---
id: svc_marketing_event
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp105
name: marketing-event
dev_owner: 陆亚东
aliases: [gp105_marketing-event]
related_services: [svc_mssii, svc_acs, svc_member]
related_tables: []
---

# marketing-event

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp105` · domain=`service-catalog`。

## 作用
营销事件（调 mssii/acs）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_mssii]] mssii（营销 / 商户消息服务） · 84052 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 42027 次 · high
- [[svc_member]] member（会员 / 账户核心） · 10528 次 · high
