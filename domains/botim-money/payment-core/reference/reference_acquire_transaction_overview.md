---
id: reference_acquire_transaction_overview
object_type: Reference
name: 收单交易业务总览
aliases: [acquire-transaction-overview]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
source_type: wiki
source_ref: confluence:AQ/997851554
tags: [payment-core, wiki-overview]
related_services: [svc_acquireii, svc_aml, svc_cashdesk_api, svc_cmf, svc_dpm_accounting, svc_dpm_manager, svc_dpm_task, svc_member, svc_merchant_fundout, svc_reconciliation, svc_router, svc_sgs, svc_tradeii]
related_tables: [tbl_acquireii_t_acquire_order]
---


# 收单交易业务总览

收单业务是支付行业的核心环节，涉及从用户支付到商户结算的整个交易流程。商户通过收单系统接入支付渠道（如银行卡支付、二维码支付、POS 终端支付等），完成资金流转、交易处理、对账和结算。

## 业务流程与全景

- 收单业务流程：覆盖用户发起支付 → 渠道处理 → 交易记账 → 清算结算的完整链路。
- 支付全景图：展示商户端、收单、支付引擎、渠道、清算等环节之间的协作关系。

## 核心概念

- **PaySceneCode（支付场景码）**：标识不同支付场景，如 JSAPI、INAPP、QRPAY 等，详见 acquire-pay-scene-code。
- **PayChannelNo（支付渠道号）**：标识不同资金渠道，如对私网银、余额、国际卡等，详见 acquire-pay-channel-no。

## 接口与测试

- SGS 接口文档：https://developers.payby.com/docs/General/integration-guide
- SGS 接口测试平台：https://qa.test2pay.com/manualTest/gateway/sgs
- 参考文档：PayBy 接口文档 v2.19、PayBy_transfer_to_bank 等。

## 应用与服务

收单交易链路涉及网关、收银台、交易、支付、风控、清算等多个应用，完整清单及负责人见 acquire-services-catalog。

## 数据库

收单交易相关核心表分布在 acquireii、tradeii、cashdesk、aml、member、dpm、cmf、router、reconciliation、mhtfundout 等库中，常用 SQL 与表说明见 acquire-database-guide。

- SIM 环境 MySQL 链接详情：http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md

## 相关链接

- 业务域：domain_acquire_transaction
