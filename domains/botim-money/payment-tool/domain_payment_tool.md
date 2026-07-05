---
id: domain_payment_tool
object_type: Domain
name: payment-tool
aliases: [channel, 渠道, Payment Tool, PT, CMF, Funds Channel, qpay]
domain: payment-tool
business_line: botim-money
status: active
owner: kingo.liang
reviewer: kingo.liang
dev_owner: kingo.liang
last_reviewed_at: '2026-06-26'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [payment-tool, channel, 渠道, qpay, CMF]
related_services: [svc_cmf, svc_cmf_task, svc_fcw, svc_router, svc_qpay_cko, svc_qpay_nipos, svc_qpay_nisocket, svc_qpay_fsii, svc_qpay_fts, svc_qpay_npss, svc_qpay_enbd, svc_qpay_zand, svc_qpay_mpgs, svc_h2h, svc_host_gateway, svc_channel_paykii, svc_channel_mobile_ding, svc_3ds2, svc_cards]
---

# payment-tool(渠道 / Funds Channel)

> 域入口。业务应用与下游银行/PSP 之间的渠道中间层,公司内部称 payment-tool 业务。owner / 研发 Payment Tool 团队(Kingo Liang / Hefei Zhang / Guoyou Ma)。

## 概述
统一管理渠道订单全生命周期:入款/出款/退款的渠道订单(CMF)、智能渠道路由(Router)、各银行/卡组织的渠道适配器(MPGS/CKO/NI/Fiserv/AANI/ENBD/Zand 等)、3DS 认证、DCC 动态货币转换、主渠道失败 Fallback、渠道对账。也维护卡 BIN 基础库(cards,授权热路径卡信息查询)。

## 本域内容
- **service/** — 渠道核心 cmf/cmf-task、回调 fcw、路由 router、适配器 qpay-cko/nipos/nisocket/fsii/npss/enbd/zand/mpgs、h2h、host-gateway、channel-paykii/mobile-ding、3ds2、卡BIN cards。
- **table/** — cmf(渠道订单)、router(结果码)、cashdesk。
- **flow/**(7)· **scenario/**(7)· **troubleshooting/**(2)。

## 相邻域
交易核心 → [[domain_payment_core]];清结算/对账 → [[domain_settlement]];汇款(同 Kingo 团队)→ [[domain_remittance]]。

## 渠道适配器索引(补)
核心渠道见 `related_services`;其余渠道适配器:[[svc_qpay_ni_channel]] / [[svc_qpay_niboarding]](NI 收单/入网)、[[svc_qpay_pl_channel]](PayLater)、[[svc_qpay_aplus]](Alipay+)、[[svc_qpay_klip]]、[[svc_qpay_mcii]]、[[svc_qpay_fs]]、[[svc_qpay_installment]](分期)、[[svc_bafl_channel]]、[[svc_kiosk_channel]](KIOSK)、[[svc_rtp]](NPSS Request-to-Pay)。

## 参考索引
- [[reference_cgs_apitest_payment_overview]](cgs-apitest payment 自动化模块总览)
- [[reference_merchant_fund_out_overview]](商户出款业务总览)· [[reference_zand_fundout_overview]](ZAND 渠道出款)
- [[reference_enbd_channel_overview]](ENBD 渠道)· [[reference_mit_cit_recurring_payment_overview]](MIT/CIT 循环支付 MPGS)
- [[reference_payby_payment_scenarios_overview]](支付场景现状梳理)

## 流程 / 场景索引
- [[flow_chargeback_process_overview]](Chargeback 端到端处理流程)· [[flow_wechat_overseas_static_qr_payment]](微信海外主扫静态码 EPCC)
- [[scn_channel_prerelease_collaboration]](渠道发布前 Dev-Test-Product 协作)· [[scn_gppc_dgpay_key_exchange]](GPPC-DGPAY 密钥交换与配置)
