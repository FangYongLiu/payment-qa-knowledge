---
id: svc_counter
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp031
name: counter
dev_owner: 夏一冰
aliases: [gp031_counter]
related_services: [svc_cards, svc_escrow, svc_vis, svc_router, svc_reconciliation, svc_dpm_accounting, svc_visii, svc_cmf]
related_tables: []
---

# counter

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp031` · domain=`payment-tools`。

## 作用
账务记账（入账 Counter，被 payment 调用）

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_cards]] cards（卡管理） · 3929 次 · high
- [[svc_escrow]] escrow（担保 / 托管交易） · 1454 次 · high
- [[svc_vis]] vis · 1215 次 · high
- [[svc_router]] router（渠道路由） · 1036 次 · high
- [[svc_reconciliation]] reconciliation（对账） · 743 次 · high
- [[svc_dpm_accounting]] dpm-accounting（账务平台记账） · 293 次 · high
- [[svc_visii]] visii · 12 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 10 次 · high

**被调用(上游)—— 这些服务调用本服务:**
payment

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
