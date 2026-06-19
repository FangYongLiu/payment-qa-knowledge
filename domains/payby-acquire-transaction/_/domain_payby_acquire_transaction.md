---
id: domain_payby_acquire_transaction
object_type: Domain
domain: acquire-transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:725ad723-2e21-421d-837b-1ac7e8e0fd3a
tags:
- 收单
- 支付
- 交易
- 清结算
subdomain: null
module: null
sensitivity: normal
name: PayBy收单交易业务域
aliases: []
related_services: []
related_tables:
- acquireii.t_acquire_order
- tradeii.t_trade_order
- cashdesk.t_group_scheme_rel
- cashdesk.t_filter_scheme
- aml.t_identity_rule
- member.tm_member
- dpm.t_dpm_outer_account_subset
- cmf.tt_cmf_order
- router.t_channel
- reconciliation.t_fund_flow
- mhtfundout.t_withdraw_order
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
PayBy 收单交易业务域覆盖商户端收单全链路：从用户发起支付，到商户接入支付渠道（银行卡支付、二维码支付、POS 终端支付等），完成资金流转、交易处理、对账与结算。该业务域是支付行业的核心环节，串联用户、商户、渠道与清结算系统。

## 覆盖范围
- **商户接入**：商户服务-sgs 前置（gp071_merchant-frontend）、商户收单服务（gp069_acquireii）、商户服务（gp044_merchant）
- **支付鉴权与收银**：收银台 v2（gp193_cashierii）、收银台 api（gp007_cashdesk-api）、支付鉴权（gp034_authpay）、核身查询（gp079_grc）、风控（gp209_aml）
- **交易处理**：服务端网关（gp028_sgs）、交易服务（gp123_tradeii）、支付前置（gp014_pfs-payment）、支付引擎（gp006_payment）、算费服务（gp003_pbs）、会员服务（gp005_member）、储值记账（gp004_dpm）
- **渠道与机构通知**：资金渠道管理（gp002_cmf）、渠道路由（gp124_router）、MPGS 渠道（gp267_qpay-mpgs）、机构通知回调（gp039_fcw）
- **清算结算与出款**：清算（gp043_reconciliation）、清算管理后台（gp031_counter）、商户出款应用（gp083_merchant-fundout）
- **支付场景**：JSAPI、INAPP、PAYPAGE、DYNQR、QRPAY、AUTODEBIT、CASHTOPUP、FACE、DIRECTPAY、EWALLET、PAYANDSIGN
- **支付渠道**：04 对私网银 / 12 对公网银 / 14 余额 / 15 快捷支付 / 16 线下汇款 / 17 MOTO / 18 KIOSK / 20 PayLater / 21 ALIPAY / 22 GP抵扣 / 23 GP支付 / 30 国际卡

## 关键服务/流程
**收单交易主链路**：
1. SGS 网关（gp028_sgs）接收商户请求，经商户前置（gp071_merchant-frontend）→ 商户收单（gp069_acquireii）落单到 `acquireii.t_acquire_order`
2. 收银台（gp193_cashierii / gp007_cashdesk-api）按 `cashdesk.t_group_scheme_rel`、`cashdesk.t_filter_scheme` 完成鉴权方案编排
3. 鉴权节点：支付鉴权（gp034_authpay）、核身查询（gp079_grc）、风控（gp209_aml，规则表 `aml.t_identity_rule`）
4. 交易服务（gp123_tradeii）生成 `tradeii.t_trade_order`，支付前置（gp014_pfs-payment）→ 支付引擎（gp006_payment）发起渠道支付
5. 算费（gp003_pbs）、会员（gp005_member，`member.tm_member`）、储值记账（gp004_dpm，`dpm.t_dpm_outer_account_subset`）配合扣款记账
6. 渠道路由（gp124_router，`router.t_channel`）→ 资金渠道管理（gp002_cmf，`cmf.tt_cmf_order`）→ 具体渠道（如 gp267_qpay-mpgs）
7. 机构回调（gp039_fcw）→ 清算（gp043_reconciliation，`reconciliation.t_fund_flow`）→ 商户出款（gp083_merchant-fundout，`mhtfundout.t_withdraw_order`）

**对外文档**：SGS 接口文档 https://developers.payby.com/docs/General/integration-guide ；SGS 测试平台 https://qa.test2pay.com/manualTest/gateway/sgs

## QA 关注点
- **PaySceneCode 与 PayChannelNo 组合**：不同场景码（JSAPI/INAPP/QRPAY/AUTODEBIT 等）配不同渠道号（如 21 ALIPAY、30 国际卡）的可用性与路由准确性
- **收单订单与交易订单一致性**：`acquireii.t_acquire_order` 与 `tradeii.t_trade_order` 的状态/金额对齐
- **鉴权方案编排**：`cashdesk.t_group_scheme_rel` × `cashdesk.t_filter_scheme` 与风控 `aml.t_identity_rule`、核身（gp079_grc）的命中链路
- **渠道路由与渠道单**：`router.t_channel` 路由结果与 `cmf.tt_cmf_order` 的渠道下单结果
- **清结算闭环**：机构回调（gp039_fcw）→ `reconciliation.t_fund_flow` 入账 → `mhtfundout.t_withdraw_order` 商户提现
- **环境与库连接**：SIM 环境 MySQL 详情见 http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md ，覆盖 acquireii / tradeii / cashdesk / aml / member / dpm / cmf / router / reconciliation / mhtfundout 等库
- **应用归属**：变更影响面需对照应用-Owner 清单（如收单 王斌、交易 唐宇、支付引擎/风控 李德文、清算 夏一冰、渠道 马国友 等）
