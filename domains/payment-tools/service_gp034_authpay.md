---
id: svc_authpay
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp034
name: authpay
dev_owner: Guoyou.Ma
aliases: [gp034_authpay]
related_services: []
related_tables: []
---

# authpay

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp034` · domain=`service-catalog`。

## 作用
授权支付 / 免密代扣执行（被 cashier/cashdesk/trade 调用）

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`service-catalog`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
cashierii, cashdesk-api, tradeii

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
