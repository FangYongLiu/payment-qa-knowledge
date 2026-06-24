---
id: svc_cashdesk_api
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp007
name: cashdesk-api
dev_owner: Guoyou.Ma
aliases: [gp007_cashdesk-api]
related_services: [svc_tradeii, svc_member, svc_grc_check_identity_provider, svc_protocol, svc_authpay, svc_cmf, svc_voucher, svc_ues_ws, svc_custom, svc_merchant, svc_cards, svc_fundout, svc_gpoint, svc_cms, svc_marketing, svc_pbs, svc_pcm, svc_acs]
related_tables: []
---

# cashdesk-api

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp007` · domain=`payment-tools`。

## 作用
统一收银台（Cashdesk）—— 收银台初始化 / 确认支付 / 协议签约 / 匿名卡支付（cardPayForAnonymous）

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_tradeii]] tradeii（交易订单引擎） · 48466 次 · high
- [[svc_member]] member（会员 / 账户核心） · 30514 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 14339 次 · med·待核实
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 9367 次 · high
- [[svc_authpay]] authpay（授权支付 / 免密代扣执行） · 7855 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 7062 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 5332 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 5188 次 · med·待核实
- [[svc_custom]] custom（客户 / 定制配置） · 4812 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 3388 次 · high
- [[svc_cards]] cards（卡管理） · 3328 次 · med·待核实
- [[svc_fundout]] fundout（出款 / 代付核心） · 2930 次 · high
- [[svc_gpoint]] gpoint · 2832 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 1414 次 · high
- [[svc_marketing]] marketing（营销服务） · 1223 次 · high
- [[svc_pbs]] pbs（计费 / 定价） · 1020 次 · high
- [[svc_pcm]] pcm · 548 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 142 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend, cmf, acquireii, cmf-task

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §3. 自动代扣 / 签约（`test_auto_debit`）

## 观测到的对外方法
cardPayForAnonymous
