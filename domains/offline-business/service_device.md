---
id: svc_device
object_type: Service
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp054
name: device
dev_owner: 王斌
aliases: [gp054_device]
related_services: [svc_ppcenter, svc_merchant]
related_tables: []
---

# device

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp054` · domain=`offline-business`。

## 作用
设备 / 产品中心接入（调 ppcenter/merchant/store）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`offline-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ppcenter]] ppcenter（产品中心） · 361089 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 9066 次 · high

**被调用(上游)—— 这些服务调用本服务:**
acquireii
