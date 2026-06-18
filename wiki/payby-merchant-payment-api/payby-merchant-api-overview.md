---
title: PayBy商户支付接口总览
domain: payby-merchant-payment-api
kind: wiki_page
slug: payby-merchant-api-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:cc03b2a8-87d2-4334-bf2e-f10ac46eed2d
tags: []
---

# PayBy商户支付接口总览

本页用于说明 PayBy 商户支付接口文档的阅读对象、版本演进与文档整体结构，便于读者快速定位所需内容。相关业务域见 [[domain_payby_merchant_payment_api]]。

## 阅读对象

面向集成 PayBy 的商户系统（在线购物平台、人工收银系统、自动化智能收银系统或其他）相关人员：

- 技术架构师
- 研发工程师
- 测试工程师
- 系统运维工程师

## 文档结构

整篇文档主要包含以下部分：

- **文档说明**：阅读对象与版本说明
- **术语**：以支付场景为核心的概念定义，详见 [[payby-payment-scenarios]]
- **接口规范**：公共参数、请求/响应规则、签名等
- **业务接口**：创建订单、查询订单、取消订单、退款、查询退款、冲正、更新订单超时时间、对账单下载、单笔付款到账户/银行卡及其查询、查询/解绑卡、查询收银台 URL、查询会员余额等
- **通知**：支付结果、退款结果、付款到账户/银行卡成功、拒付、VAM 充值等异步通知
- **返回码**：总览与各接口对应的返回码

## 版本演进概览

接口自 v2.0.0（2020-02-09 初稿）起持续迭代，演进主线包括：

### 早期基础完善（v2.0.0 ~ v2.0.18）

- 完善基础支付链路：创建订单、查询、退款、对账单
- 扩展资金出款类接口：单笔付款到账户、单笔付款到银行卡及对应查询接口、对公转账
- 新增冲正接口（v2.0.16）
- 持续补充支付场景：InApp、广告（AD）、CASHTOPUP 等
- 字段扩展：`failDes`、`secondaryMerchantId`、`deviceId`、`reserved`、`revoked` 等

### 场景与能力扩展（v2.1 ~ v2.10）

- 新增支付场景：FACE（v2.1）、DIRECTPAY（v2.2）、EWALLET（v2.6）、PAYANDSIGN（v2.11）
- 新增能力接口：查询卡信息、解绑卡（v2.5）；查询收银台 URL 信息（v2.7）
- 创建订单与退款新增 `sharingParamList`、`sharingInfoList`、`refundSharingAmount`、`feeRefunded`、`sharingRemainRefundInfoList` 等分账相关参数（v2.9 / v2.10）
- DIRECTPAY 返回 `PaymentInfo.cardinfo`；转账接口新增 `beneficiaryAddress`
- 调整 `expiredTime` 上限至 48 小时（v2.4）

### 分账与代扣代缴增强（v2.12 ~ v2.16）

- 创建订单/退款新增 `withholdAndRemitFee`
- 分账返回新增 `sharingSettledFeeAmount`、`withholdAndRemitFee`
- 新增更新订单超时时间接口（v2.14）
- DIRECTPAY 新增分期场景参数；PAYANDSIGN 新增 `customerId`
- 创建订单新增/返回 `promotionInfoList`（v2.15）

### 近期能力补强（v2.17 ~ v2.26）

- 查询会员余额接口（v2.17）
- `cardInfo` 增加 `issueCountry`、`issueBank`；`PaymentInfo` 增加 `channelParam`
- 新增 `eWalletCode` 枚举（v2.18）
- 创建订单请求新增 `subjectAr`（v2.19）
- 新增拒付通知（v2.20）、VAM 充值通知（v2.21）
- 新增微信小程序支付（v2.22）
- 新增 AFT 参数（v2.23）
- DIRECTPAY 场景支持 DevicePay（v2.24）
- 新增预授权交易；查询与商户通知返回 Auth Code、RRN、Stan、Acquire Code、Acquire Message（v2.25）
- DIRECTPAY 新增 `agreementInfo` 信息（v2.26）

## 主要业务能力索引

文档围绕以下能力组织接口与字段定义：

- **收单**：创建订单、查询订单、取消订单、更新订单超时时间、冲正
- **退款**：发起退款、查询退款（含分账退款）
- **资金出款**：单笔付款到账户/银行卡及查询、对公转账
- **卡与收银台**：查询/解绑卡、查询收银台 URL 信息
- **账户**：查询会员余额
- **对账**：下载对账单
- **异步通知**：支付/退款/付款成功、拒付、VAM 充值
- **支付场景**：JSAPI、App、支付网页、付款码、动态码、协议授权、现金充值、直联（DIRECTPAY）、FACE、EWALLET、PAYANDSIGN、预授权等，详见 [[payby-payment-scenarios]]
