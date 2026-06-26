---
title: PayBy收单交易业务总览
domain: acquire-transaction
kind: wiki_page
slug: payby-acquire-transaction-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:725ad723-2e21-421d-837b-1ac7e8e0fd3a
tags: []
related_services:
  - svc_acquireii
  - svc_aml
  - svc_authpay
  - svc_cashdesk_api
  - svc_cashierii
  - svc_cmf
  - svc_counter
  - svc_fcw
  - svc_member
  - svc_merchant
  - svc_merchant_frontend
  - svc_merchant_fundout
  - svc_payment
  - svc_pbs
  - svc_pfs_payment
  - svc_qpay_mpgs
  - svc_reconciliation
  - svc_router
  - svc_sgs
  - svc_tradeii
---

# PayBy收单交易业务总览

PayBy 商户端收单是支付业务的核心环节，覆盖从用户发起支付到商户完成结算的全链路交易处理，涉及多种支付渠道接入、资金流转、对账与清算。

## 收单业务范围

商户端收单业务通过收单系统接入多种支付渠道，完成以下核心能力：

- 银行卡支付、二维码支付、POS 终端支付等多渠道接入
- 资金流转与交易处理
- 对账与结算

## 收单业务流程

收单业务覆盖用户支付 → 渠道处理 → 商户结算的完整链路（详见原文流程图）。

## 支付全景图

支付全景围绕**支付场景码**与**支付渠道号**两大维度，对接 SGS 网关、收银台、交易、支付前置、支付引擎、清算等模块。详见 [[payby-acquire-pay-scene-codes]]。

### 接入文档与测试平台

- SGS 接口文档：https://developers.payby.com/docs/General/integration-guide
- SGS 接口测试平台：https://qa.test2pay.com/manualTest/gateway/sgs
- 参考文档：PayBy 接口文档_v2.19_20240620、PayBy_trasnfer_to_bank

## 核心模块概述

收单链路涉及的应用大致分为以下几类（完整清单与负责人见 [[payby-acquire-applications-owners]]）：

- **网关与前置层**：gp028_sgs（服务端网关）、gp071_merchant-frontend（SGS 前置）、gp014_pfs-payment（支付前置）
- **收单与收银台**：gp069_acquireii（商户收单）、gp193_cashierii（收银台 v2）、gp007_cashdesk-api（收银台 api）
- **交易与支付**：gp123_tradeii（交易服务）、gp006_payment（支付引擎）、gp034_authpay（支付鉴权）
- **算费与商户**：gp003_pbs（算费）、gp044_merchant（商户）、gp083_merchant-fundout（商户出款）
- **会员与记账**：gp005_member（会员）、gp004_dpm（储值记账）
- **核身与风控**：gp079_grc（核身查询）、gp209_aml（风控）
- **渠道与路由**：gp002_cmf（资金渠道管理）、gp124_router（渠道路由）、gp267_qpay-mpgs（MPGS 渠道）、gp039_fcw（机构通知回调）
- **清算**：gp043_reconciliation（清算）、gp031_counter（清算管理后台）

## 数据库速查

收单链路涉及 acquireii、tradeii、cashdesk、aml、member、dpm、cmf、router、reconciliation、mhtfundout 等多个库的核心表。常用表与查询示例见 [[payby-acquire-databases-guide]]。

- SIM 环境 MySQL 连接详情：http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md

## 相关页面

- [[payby-acquire-pay-scene-codes]]：PaySceneCode 与 PayChannelNo 取值清单
- [[payby-acquire-applications-owners]]：应用清单与对应负责人
- [[payby-acquire-databases-guide]]：核心表与常用 SQL
