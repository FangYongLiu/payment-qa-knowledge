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
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_online_business_direct_pay, scn_online_business_merchant_payout, scn_online_business_merchant_split, scn_online_business_pre_auth, scn_remittance_cross_border, scn_wallet_consumer_pay, scn_wallet_deposit, scn_wallet_p2p, scn_wallet_withdraw]
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
**UAT Kibana 7d INFO 观测的主要业务类**(app_id=`tradeii`,=实际在跑的业务操作 / 入口):
- `QueryTradeOrderProcessor`×527,735 — 交易订单查询
- `RefundTradeProcessor`×71,604 — 退款交易
- `VoucherClientImpl`×371,068 — 调 voucher(全局ID/幂等)
- `RiskManagerClientImpl`×133,591 — 调风控
- `MemberClientImpl`×70,467 — 调会员
- (类名为 Dubbo/RPC 处理器/门面;次数为 7d 调用量级,反映主链路。)
## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`tradeii`):
- ERROR 2187 次,主要:`FundInValidateProcessor`×1366、`CheckDccAvailabilityProcessor`×356
- WARN 565 次,主要:`AutoSettlePayStrategy`×25
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp123` · domain=`payment-core`。
