---
id: svc_cashierii
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp193
name: cashierii
dev_owner: Guoyou.Ma
aliases: [gp193_cashierii]
related_services: [svc_tradeii, svc_member, svc_grc_check_identity_provider, svc_voucher, svc_authpay, svc_merchant, svc_cashdesk_api, svc_cards, svc_pbs, svc_member_front, svc_protocol, svc_cmsii, svc_cmf, svc_mns_main, svc_qpay_lean, svc_custom, svc_npss]
related_tables: []
---

# cashierii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp193` · domain=`payment-tools`。

## 作用
收银核心（Cashier II）—— 下单 / 确认支付 / 查支付结果（queryPosPayResult），编排 tradeii/member/grc/authpay/cards

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_tradeii]] tradeii（交易订单引擎） · 155466 次 · high
- [[svc_member]] member（会员 / 账户核心） · 87360 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 53652 次 · med·待核实
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 35149 次 · high
- [[svc_authpay]] authpay（授权支付 / 免密代扣执行） · 29472 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 27105 次 · high
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 25573 次 · high
- [[svc_cards]] cards（卡管理） · 21784 次 · high
- [[svc_pbs]] pbs（计费 / 定价） · 15980 次 · high
- [[svc_member_front]] member-front（会员前置服务） · 13621 次 · high
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 13471 次 · high
- [[svc_cmsii]] cmsii（内容 / 配置管理 II） · 10665 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 10245 次 · high
- [[svc_mns_main]] mns-main（消息通知中枢） · 9005 次 · med·待核实
- [[svc_qpay_lean]] qpay-lean（Lean 渠道接入） · 2361 次 · med·待核实
- [[svc_custom]] custom（客户 / 定制配置） · 936 次 · high
- [[svc_npss]] npss（即时支付 / 账单） · 31 次 · high

**被调用(上游)—— 这些服务调用本服务:**
tradeii, acquireii

## 参与的业务场景(cgs 回归)
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）

## 关键方法 / 入口
queryPosPayResult

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp193` · domain=`payment-tools`。
