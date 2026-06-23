---
id: svc_cashierii
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp193
name: cashierii
dev_owner: 刘智斌
aliases: [gp193_cashierii]
related_services: [svc_tradeii, svc_member, svc_grc_check_identity_provider, svc_merchant, svc_authpay, svc_cmf, svc_mns_main, svc_cards, svc_voucher, svc_protocol, svc_cmsii, svc_member_front, svc_pbs, svc_qpay_lean]
related_tables: []
---

# cashierii

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp193` · domain=`payment-core`。

## 作用
收银核心（Cashier II）—— 下单 / 确认支付 / 查支付结果（queryPosPayResult），编排 tradeii/member/grc/authpay/cards

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_tradeii]] tradeii（交易订单引擎） · 767 次 · high
- [[svc_member]] member（会员 / 账户核心） · 527 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 282 次 · med·待核实
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 163 次 · high
- [[svc_authpay]] authpay（授权支付 / 免密代扣执行） · 160 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 112 次 · high
- [[svc_mns_main]] mns-main（消息通知中枢） · 91 次 · med·待核实
- [[svc_cards]] cards（卡管理） · 88 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 76 次 · high
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 56 次 · high
- [[svc_cmsii]] cmsii（内容 / 配置管理 II） · 46 次 · high
- [[svc_member_front]] member-front（会员前置服务） · 40 次 · high
- [[svc_pbs]] pbs（计费 / 定价） · 32 次 · high
- [[svc_qpay_lean]] qpay-lean（Lean 渠道接入） · 14 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
tradeii, acquireii

## 参与的业务场景(cgs 回归)
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）

## 观测到的对外方法
queryPosPayResult
