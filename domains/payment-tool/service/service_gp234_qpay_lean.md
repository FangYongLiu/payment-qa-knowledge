---
id: svc_qpay_lean
object_type: Service
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp234
name: qpay-lean
aliases: [gp234_qpay-lean]
related_services: [svc_leanlink, svc_deposit]
related_tables: []
---

# qpay-lean

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp234` · domain=`channel`。

## 作用
Lean 渠道接入（开放银行）

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`channel`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_leanlink]] leanlink · 662 次 · high
- [[svc_deposit]] deposit（充值 / 存款服务） · 110 次 · high

**被调用(上游)—— 这些服务调用本服务:**
cashierii

## 参与的业务场景(cgs 回归)
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp234` · domain=`channel`。
