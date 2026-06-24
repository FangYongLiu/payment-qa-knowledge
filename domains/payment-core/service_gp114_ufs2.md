---
id: svc_ufs2
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp114
name: ufs2
dev_owner: Yongxing.Cao
aliases: [gp114_ufs2]
related_services: []
related_tables: []
---

# ufs2

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp114` · domain=`payment-core`。

## 作用
用户文件 / 数据服务（推断：被 escrow/rdgs 调用）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
escrow, rdgs
