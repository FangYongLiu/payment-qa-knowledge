---
id: svc_cmf
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp002
name: cmf
dev_owner: 张鹤飞
aliases: [gp002_cmf]
related_services: [svc_router, svc_member, svc_grc_check_identity_provider, svc_cashdesk_api, svc_exchange, svc_ues_ws]
related_tables: []
---

# cmf

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp002` · domain=`payment-tools`。

## 作用
渠道管理与资金（Channel Mgmt & Fund）—— 经 router 选渠道，连 member/exchange/cashdesk，被 payment/trade/reconciliation/fcw 等广泛调用

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_router]] router（渠道路由） · 45109 次 · high
- [[svc_member]] member（会员 / 账户核心） · 396 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 197 次 · med·待核实
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 50 次 · high
- [[svc_exchange]] exchange（换汇 / 汇率服务） · 47 次 · med·待核实
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 45 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
reconciliation, tradeii, payment, router, fcw, cashdesk-api

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）
