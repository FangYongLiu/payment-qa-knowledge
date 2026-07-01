---
id: svc_cmf
object_type: Service
domain: payment-tool
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp002
name: cmf
dev_owner: Hefei.Zhang
aliases: [gp002_cmf]
related_services: [svc_router, svc_cards, svc_member, svc_grc_check_identity_provider, svc_exchange, svc_ues_ws, svc_cashdesk_api, svc_acs, svc_counter, svc_escrow]
related_tables: []
---

# cmf

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp002` · domain=`payment-tools`。

## 作用
渠道管理与资金（Channel Mgmt & Fund）—— 经 router 选渠道，连 member/exchange/cashdesk，被 payment/trade/reconciliation/fcw 等广泛调用

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_router]] router（渠道路由） · 4105308 次 · high
- [[svc_cards]] cards（卡管理） · 37150 次 · high
- [[svc_member]] member（会员 / 账户核心） · 24864 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 16454 次 · med·待核实
- [[svc_exchange]] exchange（换汇 / 汇率服务） · 2971 次 · med·待核实
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 2638 次 · med·待核实
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 2238 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 340 次 · high
- [[svc_counter]] counter（账务记账） · 11 次 · high
- [[svc_escrow]] escrow（担保 / 托管交易） · 11 次 · high

**被调用(上游)—— 这些服务调用本服务:**
reconciliation, tradeii, payment, router, fcw, cashdesk-api

## 涉及的 API / 数据库表
**读写的表:** [[tbl_cmf_tt_inst_order]] CMF渠道订单表 tt_inst_order、[[tbl_cmf_tt_inst_order_result]] CMF指令结果表 tt_inst_order_result

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_zand_mock_vs]](自动化:ZAND Mock VS 回调工具(Zand.java))
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_payby_cash_out]](流程:现金提现端到端流程 (Cash Out / Withdraw Cash via POS))
- [[flow_payby_withdraw_to_bank]](流程:提现到银行卡端到端流程 (Transfer to Bank Account / IBAN / Aani))
- [[flow_zand_fundout]](流程:ZAND渠道出款端到端流程(SP/SQ/VS))
- [[scn_cko_card_binding_subscription]](场景:CKO 订阅支付绑卡与签约（CKO121/CKO111）)
- [[scn_online_business_mpgs_channel]](场景:MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void))
- [[scn_online_business_zand_fundout]](场景:ZAND渠道出款测试场景(TC-001~010))
- [[ts_zand_fundout]](排障:ZAND渠道出款常见故障排查)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp002` · domain=`payment-tools`。
