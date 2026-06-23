---
id: svc_acquireii
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp069
name: acquireii
dev_owner: 王斌
aliases: [gp069_acquireii]
related_services: [svc_tradeii, svc_voucher, svc_ppcenter, svc_ues_ws, svc_marketing, svc_member, svc_cmf, svc_device, svc_cashdesk_api, svc_cashierii]
related_tables: []
---

# acquireii

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp069` · domain=`online-business`。

## 作用
收单核心（Acquire II）—— 商户订单受理 / 下单 / 退款受理，编排 tradeii、voucher、ppcenter、marketing、member

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`online-business`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_tradeii]] tradeii（交易订单引擎） · 958 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 349 次 · high
- [[svc_ppcenter]] ppcenter（产品中心） · 275 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 176 次 · med·待核实
- [[svc_marketing]] marketing（营销服务） · 136 次 · high
- [[svc_member]] member（会员 / 账户核心） · 131 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 24 次 · high
- [[svc_device]] device（设备 / 产品中心接入） · 21 次 · high
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 6 次 · high
- [[svc_cashierii]] cashierii（收银核心） · 1 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
