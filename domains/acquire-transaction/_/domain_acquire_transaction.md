---
id: domain_acquire_transaction
object_type: Domain
domain: acquire-transaction
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/997851554
tags:
- 收单
- 支付
- 商户
subdomain: null
module: null
sensitivity: normal
name: 收单交易业务域
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
商户端收单业务是支付行业的核心环节，涉及从用户支付到商户结算的整个交易流程。商户通过收单系统接入支付渠道（如银行卡支付、二维码支付、POS 终端支付等），完成资金流转、交易处理、对账和结算。

## 覆盖范围
本业务域覆盖收单交易完整链路，包括：
- 支付场景接入：JSAPI、INAPP、PAYPAGE、DYNQR、QRPAY、AUTODEBIT、CASHTOPUP、FACE、DIRECTPAY、EWALLET、PAYANDSIGN（详见 [[acquire-pay-scene-code]]）
- 支付渠道接入：04 对私网银、12 对公网银、14 余额、15 快捷支付、16 线下汇款、17 MOTO、18 KIOSK、20 PayLater、21 ALIPAY、22 GP抵扣、23 GP支付、30 国际卡（详见 [[acquire-pay-channel-no]]）
- 资金流转、交易处理、对账与结算

详见 [[acquire-transaction-overview]]。

## 关键服务/流程
收单交易业务域涉及的核心应用服务（详见 [[acquire-services-catalog]]）：
- gp028_sgs 服务端网关
- gp071_merchant-frontend 商户服务-sgs前置
- gp069_acquireii 商户收单服务
- gp193_cashierii 收银台v2
- gp007_cashdesk-api 收银台api
- gp123_tradeii 交易服务
- gp079_grc 核身查询
- gp034_authpay 支付鉴权
- gp003_pbs 算费服务
- gp044_merchant 商户服务
- gp005_member 会员服务
- gp083_merchant-fundout 商户出款应用
- gp004_dpm 储值记账
- gp209_aml 风控
- gp014_pfs-payment 支付前置
- gp006_payment 支付引擎
- gp002_cmf 资金渠道管理
- gp124_router 渠道路由
- gp267_qpay-mpgs MPGS渠道
- gp039_fcw 机构通知回调
- gp043_reconciliation 清算
- gp031_counter 清算管理后台

外部对接接口：
- SGS 接口文档：https://developers.payby.com/docs/General/integration-guide
- SGS 接口测试平台：https://qa.test2pay.com/manualTest/gateway/sgs

## QA 关注点
- 支付场景码 PaySceneCode 与支付渠道号 PayChannelNo 的组合覆盖与匹配验证
- 关键数据库表的数据流转一致性（详见 [[acquire-database-guide]]）：
  - acquireii.t_acquire_order 收单交易表
  - tradeii.t_trade_order 交易订单
  - cashdesk.t_group_scheme_rel / t_filter_scheme 收银台鉴权方案与节点
  - aml.t_identity_rule 风控核身规则
  - member.tm_member 会员信息表
  - dpm.t_dpm_outer_account_subset 商户Basic帐户-余额
  - cmf.tt_cmf_order 渠道订单
  - router.t_channel 路由渠道
  - reconciliation.t_fund_flow 入账流水
  - mhtfundout.t_withdraw_order 商户提现订单
- SIM 环境 MySQL 链接：http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md
- 收单全链路（鉴权→风控→支付引擎→渠道→清算→结算）回归与对账校验
