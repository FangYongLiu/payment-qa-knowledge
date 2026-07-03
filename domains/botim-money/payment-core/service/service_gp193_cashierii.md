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
dev_owner: Guoyou.Ma
aliases: [gp193_cashierii]
related_services: [svc_tradeii, svc_member, svc_grc_check_identity_provider, svc_voucher, svc_authpay, svc_merchant, svc_cashdesk_api, svc_cards, svc_pbs, svc_member_front, svc_protocol, svc_cmsii, svc_cmf, svc_mns_main, svc_qpay_lean, svc_custom, svc_npss]
related_tables: []
related_scenarios: [scn_online_business_cashier_pay, scn_remittance_cross_border, scn_wallet_consumer_pay, scn_wallet_deposit, scn_wallet_p2p]
---

# cashierii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp193` · domain=`payment-core`。

## 作用
收银核心（Cashier II）—— 下单 / 确认支付 / 查支付结果（queryPosPayResult），编排 tradeii/member/grc/authpay/cards

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`payment-core`

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

## 关键方法 / 入口(UAT 实测)
- `queryPosPayResult`(查 POS 支付结果);收银下单/确认;免登(unauth)链:`cache-card-info`(缓存卡→返回 `CCT:` 卡 token)→ `card-token-pay`(卡 token 支付→返回 bankForm 3ds)。
- 实测入口(cgs)前缀 `/cashierii/*`:`/cashierii/common/v1/unauth/cache-card-info`、`/cashierii/pay/v1/unauth/card-token-pay`。

## 涉及的 API / 数据库表
- **暴露/相关 API**:`/cashierii/*`(unauth 缓存卡 / 卡 token 支付 / 查结果);Dubbo facade 供 [[svc_tradeii]]/[[svc_acquireii]] 调。
- **读写的表**:收银交易 token / 支付结果(待补具体表)。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **免登收银链**:cache-card-info 返回 `CCT:<token>` → card-token-pay 提交 → 返回 `bankForm`(3ds mock TEST101)→ 轮询至 SETTLED;卡数据经 SDK 加密。
- 收银台支付方式来自 [[svc_cashdesk_api]] `unityInitPayPage`(余额/快捷卡/GPay);cashierii 执行选定方式的扣款。
- 成功后交易落 [[svc_tradeii]] `t_trade_order.trade_status='SS'`(见 [[scn_online_business_cashier_pay]])。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_bpg_paypage]](自动化:收银台 BPG PayPage 自动化)
- [[auto_online_business_dynqr]](自动化:动态二维码收银自动化)
- [[auto_online_business_qr_pay]](自动化:二维码/付款码开关自动化)
- [[auto_online_business_send_pay_link]](自动化:发送支付链接自动化)
- [[auto_online_business_smart_code]](自动化:智慧码支付自动化)
- [[auto_online_business_smart_pos]](自动化:智能 POS 自动化)
- [[auto_online_business_taxi]](自动化:出租车支付自动化)
- [[auto_remittance_remittance]](自动化:跨境汇款自动化)
- [[auto_remittance_vam]](自动化:VAM 虚拟账户自动化)
- [[auto_wallet_AA_splitting]](自动化:AA 收款自动化)
- [[auto_wallet_deposit]](自动化:钱包充值自动化)
- [[auto_wallet_friend_transfer]](自动化:好友转账自动化)
- [[auto_wallet_payment_code]](自动化:付款码自动化)
- [[auto_wallet_phoneTransfer]](自动化:手机号转账自动化)
- [[auto_wallet_ppcTransaction]](自动化:PPC 交易自动化)
- [[auto_wallet_red_pkg]](自动化:红包自动化)
- [[flow_botim_transfer]](流程:BOTIM/ToC 转账与加款端到端流程)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_cko_subscription_payment]](流程:CKO 渠道订阅支付（签约 + 支付）时序流程)
- [[flow_remittance_send_money]](流程:Send Money 端到端转账流程)
- [[scn_online_business_cashier_pay]](场景:收银台支付 (Cashier / PayPage))
- [[scn_remittance_cross_border]](场景:跨境汇款 (Remittance))
- [[scn_remittance_send_money]](场景:Send Money 转账(KYC 分支 / 退款 / 通知))
- [[scn_wallet_consumer_pay]](场景:消费者付款 (Payment Code / PPC))
- [[scn_wallet_deposit]](场景:钱包充值 (Deposit / Top-Up))
- [[scn_wallet_p2p]](场景:钱包 P2P 转账 / 红包 (Transfer & Red Packet))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp193` · domain=`payment-core`。
