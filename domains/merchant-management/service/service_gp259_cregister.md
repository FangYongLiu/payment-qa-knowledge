---
id: svc_cregister
object_type: Service
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp259
name: cregister
aliases: [gp259_cregister]
related_services: [svc_router, svc_onboarding]
related_tables: []
---

# cregister

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp259` · domain=`portal-operations`。

## 作用
收款注册 / 收款码服务（推断：下游 router 选渠道）  **(待核实:仅凭调用关系推断)**

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`portal-operations`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_router]] router（渠道路由） · 404348 次 · high
- [[svc_onboarding]] onboarding（商户 / 用户入网） · 488 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp259` · domain=`portal-operations`。
