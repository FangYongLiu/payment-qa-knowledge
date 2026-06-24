---
id: svc_ues_ws
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp001
name: ues-ws
dev_owner: Yongxing.Cao
aliases: [gp001_ues-ws]
related_services: []
related_tables: []
---

# ues-ws

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp001` · domain=`payment-core`。

## 作用
用户事件 / 数据服务（saveDataByParam）—— 被收银 / 渠道 / 通知调用

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
wechat-channel, merchant-frontend, mns-main, escrow, acquireii, cashdesk-api

## 观测到的对外方法
saveDataByParam
