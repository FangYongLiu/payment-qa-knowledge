---
id: svc_transfer
object_type: Service
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp053
name: transfer
dev_owner: 刘智斌
aliases: [gp053_transfer]
related_services: []
related_tables: []
---

# transfer

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp053` · domain=`service-catalog`。

## 作用
(本回归窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 参与的业务场景(cgs 回归)
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）
