---
id: svc_qpay_lean
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp234
name: qpay-lean
aliases: [gp234_qpay-lean]
related_services: []
related_tables: []
---

# qpay-lean

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp234` · domain=`payment-tools`。

## 作用
Lean 渠道接入（开放银行）

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`payment-tools`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
cashierii

## 参与的业务场景(cgs 回归)
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
