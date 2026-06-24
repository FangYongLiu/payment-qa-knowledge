---
id: svc_deduct
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp205
name: deduct
dev_owner: Guoyou.Ma
aliases: [gp205_deduct]
related_services: [svc_member, svc_protocol, svc_tradeii, svc_acs, svc_voucher, svc_pns, svc_cashdesk_api, svc_grc_check_identity_provider, svc_authpay, svc_mns_main, svc_cmf]
related_tables: []
---

# deduct

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp205` · domain=`service-catalog`。

## 作用
自动代扣执行（queryProtocol，调 protocol/trade）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`service-catalog`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 21450 次 · high
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 9607 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 2086 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 995 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 818 次 · high
- [[svc_pns]] pns（支付通知服务） · 675 次 · high
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 654 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 272 次 · med·待核实
- [[svc_authpay]] authpay（授权支付 / 免密代扣执行） · 225 次 · high
- [[svc_mns_main]] mns-main（消息通知中枢） · 140 次 · med·待核实
- [[svc_cmf]] cmf（渠道管理与资金） · 79 次 · high

**被调用(上游)—— 这些服务调用本服务:**
tradeii

## 参与的业务场景(cgs 回归)
- §3. 自动代扣 / 签约（`test_auto_debit`）

## 观测到的对外方法
queryProtocol
