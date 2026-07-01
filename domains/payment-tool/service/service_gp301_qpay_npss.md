---
id: svc_qpay_npss
object_type: Service
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp301
name: qpay-npss
aliases: [gp301_qpay-npss]
related_services: [svc_merchant, svc_npss_gateway]
related_tables: []
---

# qpay-npss

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp301` · domain=`channel`。

## 作用
支付渠道接入(qpay 适配器)（npss）  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`channel`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 388 次 · high
- [[svc_npss_gateway]] npss-gateway（NPSS） · 241 次 · high

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp301` · domain=`channel`。
