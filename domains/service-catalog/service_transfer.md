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

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp053` · domain=`service-catalog`。

## 作用
transfer  **(据名推断 · 待核实:无作用文字证据,但下方有观测到的调用关系)**

## 系统中的位置
- 业务域:`service-catalog`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
push-to-pay

## 参与的业务场景(cgs 回归)
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）
