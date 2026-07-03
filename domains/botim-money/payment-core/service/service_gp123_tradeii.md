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
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_online_business_direct_pay, scn_online_business_merchant_payout, scn_online_business_merchant_split, scn_online_business_pre_auth, scn_remittance_cross_border, scn_wallet_consumer_pay, scn_wallet_deposit, scn_wallet_p2p, scn_wallet_withdraw]
related_tables:
- tbl_trade_leaf_alloc
- tbl_trade_t_acq_trade_order_ext
- tbl_trade_t_compensation_event
- tbl_trade_t_control_order
- tbl_trade_t_market_method
- tbl_trade_t_order_ext
- tbl_trade_t_other_party
- tbl_trade_t_pay_method
- tbl_trade_t_payment_order
- tbl_trade_t_payment_party
- tbl_trade_t_rfd_trade_order_ext
- tbl_trade_t_split_party
- tbl_trade_t_task_config
- tbl_trade_t_trade_batch_order
- tbl_trade_t_trade_order
- tbl_trade_t_trade_order_setting
- tbl_trade_t_trade_status_his
- tbl_tradeii_leaf_alloc
- tbl_tradeii_t_compensation_event
- tbl_tradeii_t_pay_order
- tbl_tradeii_t_payment_relate_order
- tbl_tradeii_t_product_account_config
- tbl_tradeii_t_product_config
- tbl_tradeii_t_refund_control
- tbl_tradeii_t_refund_order
- tbl_tradeii_t_refund_party
- tbl_tradeii_t_refund_pay_order
- tbl_tradeii_t_trade_marketing
- tbl_tradeii_t_trade_order
- tbl_tradeii_t_trade_order_extend
- tbl_tradeii_t_trade_order_extend_item
- tbl_tradeii_t_trade_party
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
- **暴露/相关 API**:Dubbo Facade(无对外 REST),核心 `createCashierTrade` / `queryTradeOrder` / `queryRefundOrder` / `refund` / `confirmPay`;收单经 [[svc_acquireii]] 调入。
- **核心表**:[[tbl_tradeii_t_trade_order]](交易主单)、[[tbl_tradeii_t_pay_order]]、[[tbl_tradeii_t_refund_order]] 等(见 `related_tables`)。

## 测试要点 / 排障 / 常见问题(UAT 实测语义,2026-07-03)
`t_trade_order` 是收单/支付成功判定的中枢表,实测字段口径:
- **`trade_status='SS'` = 交易成功**(收单各场景成功态的统一判定;失败/处理中为其它值)。
- **`client_id='acquire2'`** = 来源为收单(区别于钱包等其它 client)。
- **`biz_product_code`** 标识业务:`200101`(PAYPAGE/BPG)、`200104`(DirectPay)、`200111`(PreAuth/Capture);与 acquireii `product_code` 对应。
- **凭证链**:`trade_request_no`=收单 orderNo;`trade_voucher_no`(交易凭证);`pay_voucher_no`(支付凭证 311…)→ `settle_voucher_no`(结算凭证 311…);排障按凭证号跨库串联(见 [[ts_payment_db_navigation]])。
- **`control_extension`** 关键标志:`transferRule=payee:ACQUIRE_SETTLE`(收单结算给收款方)、`multiPayer=Y`(收银台多支付方)、`preauthCapture=Y` + `authorizeRequestNo`(请款关联原授权,见 [[scn_online_business_pre_auth]])。
- 退款:定时任务 `退付款` → `refund` → [[svc_pfs_payment]] 反向清分;退款单落 `t_refund_order`。
- **怎么测**:下单后按 `trade_request_no=orderNo` 查 `t_trade_order`,断言 `trade_status='SS'` + `biz_product_code` + 凭证链齐全;预授权断言 `preauthCapture` 标志。

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
- [[flow_remittance_pix_mpc]](流程:PIX MPC 商户呈现码扫码支付端到端流程)
- [[flow_remittance_send_money]](流程:Send Money 端到端转账流程)
- [[flow_wallet_send_money]](流程:Wallet Send Money 转账(KYC结算 / 过期退款))
- [[flow_wps_company_onboarding_to_payroll]](流程:WPS 企业入驻到发薪端到端流程)
- [[scn_online_business_auto_debit]](场景:自动代扣 / 签约 (Auto Debit))
- [[scn_online_business_cashier_pay]](场景:收银台支付 (Cashier / PayPage))
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_merchant_payout]](场景:商户出款 / 转账 (Transfer / Payout))
- [[scn_online_business_merchant_split]](场景:商户分账 (Merchant Split))
- [[scn_online_business_mpgs_channel]](场景:MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void))
- [[scn_online_business_pre_auth]](场景:预授权 / 请款 (PreAuth-Capture))
- [[scn_remittance_cross_border]](场景:跨境汇款 (Remittance))
- [[scn_remittance_send_money]](场景:Send Money 转账(KYC 分支 / 退款 / 通知))
- [[scn_wallet_consumer_pay]](场景:消费者付款 (Payment Code / PPC))
- [[scn_wallet_deposit]](场景:钱包充值 (Deposit / Top-Up))
- [[scn_wallet_p2p]](场景:钱包 P2P 转账 / 红包 (Transfer & Red Packet))
- [[scn_wallet_withdraw]](场景:钱包提现 (Withdraw))
- [[ts_payment_db_navigation]](排障:支付链路数据库库表速查与排查导航)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp123` · domain=`payment-core`。
