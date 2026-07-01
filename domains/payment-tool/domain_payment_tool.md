---
id: domain_payment_tool
object_type: Domain
name: payment-tool
aliases: [channel, 渠道, Payment Tool, PT, CMF, Funds Channel, qpay]
domain: payment-tool
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
