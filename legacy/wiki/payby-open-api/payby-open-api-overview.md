---
title: PayBy 开放接口文档总览
domain: payby-open-api
kind: wiki_page
slug: payby-open-api-overview
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p2
tags: []
---

# PayBy 开放接口文档总览

本页是 PayBy 商户开放接口（Open API）文档的总入口，介绍文档定位、整体范围与版本演进索引。

## 文档定位

- 面向接入 PayBy 的商户与开发者，提供收单、退款、转账、对账、卡管理等业务接口的统一说明。
- 接口文档以版本化方式持续维护，每次发布会同步更新参数、返回码、支付场景等内容。

## 业务范围

文档覆盖的主要能力包括：

- **收单与订单管理**：创建订单、查询订单、取消订单、冲正、更新订单超时时间。
- **退款**：发起退款、查询退款订单、退款结果通知。
- **转账（付款）**：单笔付款到账户、单笔付款到银行卡，及其查询接口与成功通知。
- **对账**：下载对账单接口。
- **卡与会员**：查询卡信息、解绑卡、查询收银台 URL 信息、查询会员余额。
- **分账与营销**：分账参数（sharingParamList / sharingInfoList）、代扣代缴费用（withholdAndRemitFee）、促销信息（promotionInfoList）。
- **通知类**：支付结果通知、退款结果通知、付款成功通知。

## 支付场景

文档随版本不断扩充支付场景，已覆盖的典型场景包括：

- PAYPAGE（网页支付）
- JSAPI
- InApp
- CASHTOPUP
- FACE
- DIRECTPAY（含分期等场景参数）
- EWALLET
- PAYANDSIGN（支付并签约）

每个支付场景有各自的 paySceneParams 参数集合（如 oneTimePayment、customerId、installment 等）。

## 通用约定

- 所有接口共享统一的请求参数规定（签名、公共头、请求体结构等）与返回码体系。
- 商户订单号、退款商户订单号长度统一为 64 位；订单号相关字段在多版本中有过长度与描述调整。
- 返回码按接口归类，便于排查；新增能力通常伴随对应返回码扩充。

## 版本与变更

- 文档采用 vX.Y(.Z) 形式持续迭代，从 v2.0.0（2020-02-09 初稿）至 v2.18（2024-03-04）。
- 每个版本明确列出新增/调整的字段、支付场景、返回码与接口。
- 完整的版本演进、修改点逐项清单见 [[payby-open-api-changelog]]。

## 阅读建议

- 首次接入：先了解通用请求/响应结构与签名规则，再按业务选择对应支付场景与接口。
- 已接入升级：对照 [[payby-open-api-changelog]] 检查新增字段、返回码与场景参数的兼容性影响。
- 排查问题：以接口返回码为入口，结合订单状态（如 REFUNDED_SETTLED 等）与通知回调内容定位。
