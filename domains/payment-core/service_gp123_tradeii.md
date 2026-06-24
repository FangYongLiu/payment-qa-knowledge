---
id: svc_tradeii
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp123
name: tradeii
dev_owner: Yu.Tang
aliases: [gp123_tradeii]
related_services: [svc_voucher, svc_member, svc_cmf, svc_pfs_payment, svc_cashierii, svc_pbs, svc_acs, svc_cards, svc_css, svc_authpay, svc_cms, svc_deduct, svc_ppcenter, svc_merchant]
related_tables: []
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_online_business_direct_pay, scn_online_business_merchant_payout, scn_online_business_merchant_split, scn_online_business_pre_auth, scn_remittance_cross_border, scn_wallet_consumer_pay, scn_wallet_deposit, scn_wallet_p2p, scn_wallet_withdraw, scn_channel_fund_in]
---

# tradeii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp123` · domain=`payment-core`。

## 作用
交易订单引擎（Trade II）—— 创建 / 查询交易、退款、收银交易（queryTradeOrder/createCashierTrade/refund），编排 voucher/cmf/pbs/acs/cards/cashier/pfs

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 1048225 次 · high
- [[svc_member]] member（会员 / 账户核心） · 179368 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 126532 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 33729 次 · high
- [[svc_cashierii]] cashierii（收银核心） · 20320 次 · high
- [[svc_pbs]] pbs（计费 / 定价） · 18628 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 13086 次 · high
- [[svc_cards]] cards（卡管理） · 9924 次 · high
- [[svc_css]] css（客服系统） · 7573 次 · high
- [[svc_authpay]] authpay（授权支付 / 免密代扣执行） · 1626 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 1624 次 · high
- [[svc_deduct]] deduct（自动代扣执行） · 1577 次 · high
- [[svc_ppcenter]] ppcenter（产品中心） · 636 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 633 次 · high

**被调用(上游)—— 这些服务调用本服务:**
acquireii, cashierii, cashdesk-api, remittance, merchant-fundout, deduct

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §3. 自动代扣 / 签约（`test_auto_debit`）
- §7. 跨境汇款（toC，`test_remittance`）

## 关键方法 / 入口
queryTradeOrder, queryRefundOrder, createCashierTrade, refund

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp123` · domain=`payment-core`。
