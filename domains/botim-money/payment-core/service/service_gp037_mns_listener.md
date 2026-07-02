---
id: svc_mns_listener
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
name: mns-listener
dev_owner: Yadong.Lu
aliases: [gp037_mns-listener]
related_services: [svc_mns_main, svc_ues_ws]
related_tables: []
---

# mns-listener

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp037` · domain=`payment-core`。

## 作用
消息通知监听（MailNotify/SnsNotify，转 mns-main）

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_mns_main]] mns-main（消息通知中枢） · 251333 次 · med·待核实
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 3314 次 · med·待核实

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp037` · domain=`payment-core`。
