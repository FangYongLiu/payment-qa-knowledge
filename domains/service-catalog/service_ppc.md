---
id: svc_ppc
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp212
name: ppc
dev_owner: 唐宇
aliases: [gp212_ppc]
related_services: []
related_tables: []
---

# ppc

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp212` · domain=`service-catalog`。

## 作用
(本回归窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
