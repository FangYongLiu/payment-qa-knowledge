---
id: svc_pns
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp013
name: pns
dev_owner: Guoyou.Ma
aliases: [gp013_pns]
related_services: []
related_tables: []
---

# pns

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp013` · domain=`service-catalog`。

## 作用
支付通知服务（notifyMerchant）—— 支付结果异步回调商户

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`service-catalog`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 观测到的对外方法
notifyMerchant
