---
id: svc_payment
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp006
name: payment
dev_owner: Dewen.Li
aliases: [gp006_payment]
related_services: [svc_dpm_manager, svc_cmf, svc_counter, svc_pfs_payment, svc_member]
related_tables: []
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_online_business_direct_pay, scn_online_business_merchant_payout, scn_online_business_merchant_split, scn_online_business_pre_auth, scn_remittance_cross_border, scn_wallet_consumer_pay, scn_wallet_deposit, scn_wallet_p2p, scn_wallet_withdraw]
---

# payment

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp006` · domain=`payment-core`。

## 作用
支付中台 —— 支付指令处理，编排 dpm（记账）/cmf（渠道）/pfs（履约）/counter

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_dpm_manager]] dpm-manager（账务平台管理） · 1345693 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 482556 次 · high
- [[svc_counter]] counter（账务记账） · 240539 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 214740 次 · high
- [[svc_member]] member（会员 / 账户核心） · 52669 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
pfs-payment

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_payby_payment_create_order]] PayBy创建支付订单接口
**读写的表:** [[tbl_grc_t_payment_event]] GRC支付事件表 t_payment_event_<yyyy>

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_auto_debit]](自动化:自动代扣自动化)
- [[auto_online_business_bpg_paypage]](自动化:收银台 BPG PayPage 自动化)
- [[auto_online_business_direct_pay]](自动化:直连支付自动化)
- [[auto_online_business_dynqr]](自动化:动态二维码收银自动化)
- [[auto_online_business_merchant_split]](自动化:商户分账自动化)
- [[auto_online_business_pre_auth_capture]](自动化:预授权/请款自动化)
- [[auto_online_business_qr_pay]](自动化:二维码/付款码开关自动化)
- [[auto_online_business_send_pay_link]](自动化:发送支付链接自动化)
- [[auto_online_business_smart_code]](自动化:智慧码支付自动化)
- [[auto_online_business_smart_pos]](自动化:智能 POS 自动化)
- [[auto_online_business_taxi]](自动化:出租车支付自动化)
- [[auto_online_business_transfer_order]](自动化:转账下单自动化)
- [[auto_online_business_transfer_to_bank]](自动化:转账到银行自动化)
- [[auto_online_business_transfer_to_card]](自动化:转账到卡自动化)
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
- [[flow_botim_transfer]](流程:BOTIM/ToC 转账与加款端到端流程)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_payby_cash_out]](流程:现金提现端到端流程 (Cash Out / Withdraw Cash via POS))
- [[flow_payby_withdraw_to_bank]](流程:提现到银行卡端到端流程 (Transfer to Bank Account / IBAN / Aani))
- [[scn_online_business_auto_debit]](场景:自动代扣 / 签约 (Auto Debit))
- [[scn_online_business_cashier_pay]](场景:收银台支付 (Cashier / PayPage))
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_merchant_payout]](场景:商户出款 / 转账 (Transfer / Payout))
- [[scn_online_business_merchant_split]](场景:商户分账 (Merchant Split))
- [[scn_online_business_pre_auth]](场景:预授权 / 请款 (PreAuth-Capture))
- [[scn_remittance_cross_border]](场景:跨境汇款 (Remittance))
- [[scn_wallet_consumer_pay]](场景:消费者付款 (Payment Code / PPC))
- [[scn_wallet_deposit]](场景:钱包充值 (Deposit / Top-Up))
- [[scn_wallet_p2p]](场景:钱包 P2P 转账 / 红包 (Transfer & Red Packet))
- [[scn_wallet_withdraw]](场景:钱包提现 (Withdraw))
- [[scn_wallet_withdraw_to_bank]](场景:提现到银行卡场景 (Transfer to Bank Account 字段/状态/限额/测试))
- [[ts_directpay_3ds_downgrade_token_invalid]](排障:DirectPay 3DS 降级导致 CardToken 代扣失败)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp006` · domain=`payment-core`。
