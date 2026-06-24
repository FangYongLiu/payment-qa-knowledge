---
id: svc_qpay_cko
object_type: Service
domain: acquiring
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp221
name: qpay-cko
aliases: [gp221_qpay-cko]
related_services: [svc_cards, svc_grc_check_identity_provider]
related_tables: []
---

# qpay-cko

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp221` · domain=`acquiring`。

## 作用
Checkout.com（CKO）渠道接入

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`acquiring`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cards]] cards（卡管理） · 380 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 380 次 · med·待核实

## 参与的业务场景(cgs 回归)
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）
