---
id: svc_credit_business
object_type: Service
domain: quantix
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp130
name: credit-business
dev_owner: Xiaopei.Yan
aliases: [gp130_credit-business]
related_services: [svc_member]
related_tables: []
---

# credit-business

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp130` · domain=`quantix`。

## 作用
信贷业务（调 member(Ma)）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`quantix`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 204477 次 · med·待核实
