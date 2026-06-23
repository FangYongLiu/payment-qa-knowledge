---
title: 收单交易相关应用服务清单
domain: payby-core-systems
kind: wiki_page
slug: acquire-services-catalog
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PCW/124555769
tags: []
---

# 收单交易相关应用服务清单

本页汇总收单链路涉及的微服务应用、用途说明与负责人，便于在排查交易、对接联调时快速定位。完整业务背景见 [[acquire-transaction-overview]]。PayBy 全量微服务清单见 [[payby-microservice-catalog]]。

## 应用清单

| Application | Description | Owner |
|---|---|---|
| gp028_sgs | 服务端网关 / Server Gateway，接收商户后台服务器请求 | 喻赛 |
| gp024_cgs | 客户端网关 / Client Gateway，面向 SDK/H5 暴露 HTTP API，包含验签、加解密转换、限流等 | 喻赛 |
| gp071_merchant-frontend | 商户服务-sgs 前置 | 王斌 |
| gp069_acquireii | 商户收单服务 | 王斌（沈阅） |
| gp193_cashierii | 收银台 v2，提供 App / PayPage / POS 的收银相关 API，含风控识别、商户鉴权与支付流程 | 刘智斌 |
| gp007_cashdesk-api | 旧收银台 / Cashdesk service，多数功能已被 cashierii 取代，但收银台提现流程仍保留 | 刘智斌 / 高一春 |
| gp123_tradeii | 交易服务 / Trade service，提供基础交易 API，支持需要/不需要收银台的支付场景 | 唐宇 |
| gp011_deposit | 存款 / 充值服务，为钱包、VIS、Kiosk 提供 top-up API | 唐宇 |
| gp012_fundout | 出款 / 提现服务，为钱包及商户提供基础 fundout API | 唐宇 |
| gp032_personal | 个人应用，提供钱包 top-up、withdrawal 等服务 | 喻赛 |
| gp053_transfer | 转账服务，提供钱包转账、拆账、红包等业务能力 | 刘智斌 |
| gp079_grc-component-connect-provider | 风控 / 核身查询，为支付与非支付链路提供风险控制服务 | 李德文 |
| gp034_authpay | 支付鉴权 / 收银台鉴权 | 刘智斌 / 高一春 |
| gp003_pbs | 算费服务 | 黄美美 |
| gp044_merchant | 商户服务 | 黄林伟 |
| gp005_member (ma-web) | 会员服务 / Member service，提供会员信息存储查询验证、储值账户开立与状态变更 | 陆亚东 / 沈纲领 |
| gp083_merchant-fundout | 商户出款应用 | 王斌 |
| gp004_dpm-accounting | 储值记账，提供科目与账户管理、复式记账、缓冲入账 | 周聪 |
| gp209_aml | 风控 (AML) | 李德文 |
| gp014_pfs-payment | 支付前置 / Payment front service，配合 payment 提供更具体的支付集成 API | 李德文 |
| gp006_payment | 支付引擎 / Payment engine service，控制支付流程并配置清算规则 | 李德文 |
| gp002_cmf | 资金渠道管理，统一支付接口、资金渠道路由与补单 | 张鹤飞 / 马国友 / 王迁 |
| gp002_cmf-task | 资金渠道管理定时任务，处理渠道订单相关 scheduled jobs | 张鹤飞 / 马国友 |
| gp124_router | 渠道路由 | 马国友 |
| gp267_qpay-mpgs | MPGS 渠道 | 马国友 |
| gp221_qpay-cko | Fund-in 渠道适配器之一 | - |
| gp062_h2h | Fund-out 渠道适配器之一 | - |
| gp039_fcw | 机构通知回调 / 资金渠道 webhook，统一接收渠道支付结果通知 | 马国友 / 王迁 |
| gp043_reconciliation | 清算 | 夏一冰 |
| gp031_counter | 清算管理后台 / 资金管理平台，供清算人员处理账务、对账、补单、出款等 | 夏一冰 / 王迁 |

## 按链路环节归类

- **接入层**：`gp028_sgs`、`gp024_cgs`、`gp071_merchant-frontend`
- **收单与交易**：`gp069_acquireii`、`gp123_tradeii`、`gp011_deposit`、`gp012_fundout`
- **收银台与鉴权**：`gp193_cashierii`、`gp007_cashdesk-api`、`gp034_authpay`
- **业务应用**：`gp032_personal`、`gp053_transfer`
- **风控与核身**：`gp079_grc-component-connect-provider`、`gp209_aml`
- **商户与会员**：`gp044_merchant`、`gp005_member`、`gp083_merchant-fundout`
- **计费与记账**：`gp003_pbs`、`gp004_dpm-accounting`
- **支付引擎与渠道**：`gp014_pfs-payment`、`gp006_payment`、`gp002_cmf`、`gp002_cmf-task`、`gp124_router`、`gp267_qpay-mpgs`、`gp221_qpay-cko`、`gp062_h2h`、`gp039_fcw`
- **清算**：`gp043_reconciliation`、`gp031_counter`

## 相关参考

- 接入侧场景标识见 [[acquire-pay-scene-code]]
- 渠道侧标识见 [[acquire-pay-channel-no]]
- 各应用对应的库表查询见 [[acquire-database-guide]]
- 全量微服务清单见 [[payby-microservice-catalog]]
