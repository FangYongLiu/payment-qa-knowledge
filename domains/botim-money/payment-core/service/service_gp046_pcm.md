---
id: svc_pcm
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp046
name: pcm
dev_owner: Yu.Tang
aliases: [gp046_pcm]
related_services: [svc_pcs, svc_ues_ws]
related_tables: []
---

# pcm

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp046` · domain=`payment-core`。

## 作用
pcm  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_pcs]] pcs · 178 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 162 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
cashdesk-api

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp046` · domain=`payment-core`。
