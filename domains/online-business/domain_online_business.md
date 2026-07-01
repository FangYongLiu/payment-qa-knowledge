---
id: domain_online_business
object_type: Domain
name: online-business
aliases: [线上业务]
domain: online-business
product: payment
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [online-business, 线上业务]
related_services: [svc_fundout, svc_xbh_gateway, svc_merchant_console_frontend, svc_cash_eatm, svc_customer_frontend, svc_acquireii, svc_merchant_fundout, svc_adtaxi, svc_statementii, svc_preauth, svc_pos_exception_processor, svc_acquire2_query, svc_merchant_settlement, svc_jollychic_service]
---

# online-business(线上业务)

> 业务域总览(入口节点)。owner fangyong.liu。细节见各服务对象。

## 概述
线上业务域:收单(acquiring)、出款(fundout)、商户/客户前端、收银(cash-eatm)、预授权、POS 异常处理、对账单等线上经营能力。

## 覆盖范围
共 14 个服务:fundout、xbh-gateway、merchant-console-frontend、cash-eatm、customer-frontend、acquireii、merchant-fundout、adtaxi、statementii、preauth、pos-exception-processor、acquire2-query、merchant-settlement、jollychic-service。

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
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
- [[auto_online_business_zand_mock_vs]](自动化:ZAND Mock VS 回调工具(Zand.java))
- [[flow_botim_transfer]](流程:BOTIM/ToC 转账与加款端到端流程)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_chargeback_file_processing]](流程:Chargeback拒付文件处理端到端流程)
- [[flow_merchant_fundout]](流程:商户出款端到端流程 (Merchant Fund-Out))
- [[flow_pos_scan_payment_code]](流程:付款码被 POS 机扫(线下被扫收单)端到端流程)
- [[flow_wallet_send_money]](流程:Wallet Send Money 转账(KYC结算 / 过期退款))
- [[flow_zand_fundout]](流程:ZAND渠道出款端到端流程(SP/SQ/VS))
- [[scn_online_business_auto_debit]](场景:自动代扣 / 签约 (Auto Debit))
- [[scn_online_business_cashier_pay]](场景:收银台支付 (Cashier / PayPage))
- [[scn_online_business_chargeback_file_intake]](场景:Chargeback拒付文件上传与匹配场景)
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_merchant_async_notify]](场景:商户异步通知接收与重试 (Open API))
- [[scn_online_business_merchant_payout]](场景:商户出款 / 转账 (Transfer / Payout))
- [[scn_online_business_merchant_split]](场景:商户分账 (Merchant Split))
- [[scn_online_business_mpgs_channel]](场景:MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void))
- [[scn_online_business_openapi_protocol_signing]](场景:商户 Open API 接入协议与签名/加密规则)
- [[scn_online_business_payment_code_scan]](场景:付款码被扫线下收单 (POS / 扫码枪))
- [[scn_online_business_pre_auth]](场景:预授权 / 请款 (PreAuth-Capture))
- [[scn_online_business_transaction_db_check]](场景:商户交易落库检查 (Transaction DB Check))
- [[scn_online_business_zand_fundout]](场景:ZAND渠道出款测试场景(TC-001~010))
- [[ts_acquire_order_slow_sql]](排障:收单订单查询慢SQL(t_acquire_order 大商户时间范围查询))
- [[ts_zand_fundout]](排障:ZAND渠道出款常见故障排查)
