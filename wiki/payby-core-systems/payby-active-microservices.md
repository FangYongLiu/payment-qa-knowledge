---
title: PayBy 活跃微服务清单
domain: payby-core-systems
kind: wiki_page
slug: payby-active-microservices
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:2bc88b9d-fdd4-46f9-a4aa-7ef0774c7418
tags: []
---

# PayBy 活跃微服务清单

本页列出由 OPS 团队维护的活跃 PayBy 微服务，按职能分组，包含服务编号、用途与参考链接。完整全景（含已废弃）见 [[payby-microservice-catalog]]，按业务域分类视图见 [[payby-service-category-map]]。

## 网关层

- **gp024_cgs**（Client Gateway Service）：为 SDK 客户端或 H5 暴露 HTTP API 服务；按配置将请求路由到各业务服务；包含签名验证、加解密转换、限流控制等。参考：cgs-Client Gateway。

## 钱包与个人应用

- **gp032_personal**：提供钱包相关服务，包括 top-up、withdrawal 等。参考：personal-个人应用。
- **gp053_transfer**：为业务提供转账能力，如 wallet transfer、split bill、red packet 等。参考：53-transfer。

## 充值与提现

- **gp011_deposit**：为 wallet、vis、kiosk 提供基础 deposit(top-up) API；同时承担 top-up 业务服务。参考：deposit-充值服务。
- **gp012_fundout**：为 wallet 与 merchant 提供基础 fundout API；同时承担 withdraw 业务服务。参考：fundout-提现服务。

## 交易与收银台

- **gp123_tradeii**：为需要交易与支付的业务服务提供基础 trade API；支持需要或不需要 checkout 的支付场景。参考：tradeii-API Integration。
- **gp193_cashierii**：向 app、paypage 与 pos 提供 checkout 相关 API；包含风险识别、商户认证与支付流程。参考：cashier-收银台。
- **gp007_cashdesk-api**：旧版收银台服务，多数功能已被 cashierii 替代；不包含 cashier withdraw 流程。参考：收银台接口目录。

## 支付与清算

- **gp014_pfs-payment**：与 payment 协同，为支付集成提供更具体的 API。参考：21-pfs-支付前置。
- **gp006_payment**：提供支付流程控制与清算规则配置。参考：02-Clearing Rule。
- **gp004_dpm-accounting**：提供记账能力，包含科目与账户管理、复式记账、缓冲记账。参考：31-dpm-储值。

## 风控

- **gp079_grc-component-connect-provider**：为支付与非支付场景提供风控服务。参考：11-风控。

## 资金渠道

- **gp002_cmf**（Channel Management Foundation）：管理 fund-in 与 fund-out 的资金渠道。参考：b-cmf。
- **gp002_cmf-task**（Channel Management Foundation Task）：与渠道订单相关的定时任务。参考：b-cmf。
- **gp039_fcw**：提供资金渠道 web book 服务，用于接收资金渠道厂商的支付结果。参考：d-fcw。
- **gp221_qpay-cko**：fund-in 渠道适配器之一。
- **gp062_h2h**：fund-out 渠道适配器之一。
