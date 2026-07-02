---
id: svc_member
object_type: Service
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp005
name: member
dev_owner: Yadong.Lu
aliases: [gp005_member]
related_services: [svc_dpm_accounting, svc_ccdpm_accounting, svc_cms, svc_kyc, svc_acs, svc_pts, svc_cards]
related_tables: [tbl_member_tr_deduct_channel]
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_remittance_cross_border, scn_wallet_consumer_pay, scn_wallet_deposit, scn_wallet_p2p, scn_wallet_withdraw]
---

# member

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp005` · domain=`payment-core`。

## 作用
会员 / 账户核心 —— 开户 / 查账户 / 校验支付密码 / 受益人（openAccount/checkPassword/queryAccountById），下游 dpm-accounting

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_dpm_accounting]] dpm-accounting（账务平台记账） · 3401522 次 · high
- [[svc_ccdpm_accounting]] ccdpm-accounting（加密货币账务记账） · 60299 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 4806 次 · high
- [[svc_kyc]] kyc（实名认证） · 814 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 390 次 · high
- [[svc_pts]] pts · 238 次 · high
- [[svc_cards]] cards（卡管理） · 2 次 · high

**被调用(上游)—— 这些服务调用本服务:**
remittance, pfs-payment, reconciliation, credit-business, merchant-frontend, tradeii

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_payby_get_member_balance]] 查询会员余额接口、[[api_member_query_eid_bound_account]] 查询EID绑定手机账户接口、[[api_member_change_mobile_refresh_kyc]] 变更手机并刷新KYC接口
**读写的表:** [[tbl_member_tr_bank_card_token]] 银行卡签约Token表、[[tbl_member_tr_deduct_channel]] 代扣渠道表 tr_deduct_channel、[[tbl_member_db]] 会员相关库(member)核心表

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）
- §7. 跨境汇款（toC，`test_remittance`）
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）

## 关键方法 / 入口
queryAccountById, queryMemberIntegratedInfo, openAccount, queryAccountByMemberId, checkPassword, queryBeneficiaryConfig

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_auto_debit]](自动化:自动代扣自动化)
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
- [[auto_wallet_withdraw]](自动化:钱包提现自动化)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_kyc_change_mobile]](流程:KYC 换绑手机号端到端流程 (Change Mobile))
- [[flow_merchant_onboarding]](流程:商户注册与入驻端到端流程(Acquire + WPS))
- [[scn_online_business_auto_debit]](场景:自动代扣 / 签约 (Auto Debit))
- [[scn_online_business_cashier_pay]](场景:收银台支付 (Cashier / PayPage))
- [[scn_remittance_cross_border]](场景:跨境汇款 (Remittance))
- [[scn_wallet_consumer_pay]](场景:消费者付款 (Payment Code / PPC))
- [[scn_wallet_deposit]](场景:钱包充值 (Deposit / Top-Up))
- [[scn_wallet_p2p]](场景:钱包 P2P 转账 / 红包 (Transfer & Red Packet))
- [[scn_wallet_withdraw]](场景:钱包提现 (Withdraw))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp005` · domain=`payment-core`。
