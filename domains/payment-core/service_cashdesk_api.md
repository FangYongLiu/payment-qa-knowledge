---
id: svc_cashdesk_api
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp007
name: cashdesk-api
dev_owner: 刘智斌
aliases: [gp007_cashdesk-api]
related_services: [svc_tradeii, svc_member, svc_grc_check_identity_provider, svc_protocol, svc_cmf, svc_authpay, svc_voucher, svc_ues_ws, svc_custom, svc_cards, svc_merchant, svc_fundout, svc_cms, svc_pbs, svc_marketing]
related_tables: []
---

# cashdesk-api

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp007` · domain=`payment-core`。

## 作用
统一收银台（Cashdesk）—— 收银台初始化 / 确认支付 / 协议签约 / 匿名卡支付（cardPayForAnonymous）

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_tradeii]] tradeii（交易订单引擎） · 648 次 · high
- [[svc_member]] member（会员 / 账户核心） · 592 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 280 次 · med·待核实
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 208 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 166 次 · high
- [[svc_authpay]] authpay（授权支付 / 免密代扣执行） · 150 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 114 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 112 次 · med·待核实
- [[svc_custom]] custom（客户 / 定制配置） · 80 次 · high
- [[svc_cards]] cards（卡管理） · 74 次 · med·待核实
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 56 次 · high
- [[svc_fundout]] fundout（出款 / 代付核心） · 48 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 16 次 · high
- [[svc_pbs]] pbs（计费 / 定价） · 16 次 · high
- [[svc_marketing]] marketing（营销服务） · 15 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend, cmf, acquireii, cmf-task

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §3. 自动代扣 / 签约（`test_auto_debit`）

## 观测到的对外方法
cardPayForAnonymous
