---
id: svc_mns_scheduler
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp037
name: mns-scheduler
dev_owner: Yadong.Lu
aliases: [gp037_mns-scheduler]
related_services: [svc_ues_ws, svc_member]
related_tables: []
---

# mns-scheduler

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp037` · domain=`payment-core`。

## 作用
消息通知调度（定时通知，调 ues）

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 1688 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 6 次 · high
