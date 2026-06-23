---
title: PayBy支付场景术语
domain: payby-open-api
kind: wiki_page
slug: payby-payment-scenarios
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:cc03b2a8-87d2-4334-bf2e-f10ac46eed2d
tags: []
---

# PayBy支付场景术语

本页汇总 PayBy 商户支付接口中涉及的各类支付场景术语定义，便于理解不同业务模式下的接入方式与适用范围。相关接口与字段细节请参见 [[payby-merchant-api-overview]]。

## JSAPI 支付

商户已经有 H5 商城网站，用户在 PayBy 内访问时，可以调用 PayBy 完成下单购买流程。

## App 支付

又称移动端支付。商户在移动端应用 APP 中集成开放 SDK，调起 PayBy 模块完成支付。

## 支付网页支付（PAYPAGE）

主要在手机、ipad、电脑等设备中，通过浏览器跳转到 PayBy 支付网页完成支付。

## 付款码支付

用户展示 PayBy 内的"付款码"，由商户系统扫描后直接完成支付。

- 主要应用于线下面对面收银场景。

## 动态码支付

商户系统按 PayBy 协议生成支付二维码，用户使用 PayBy"扫一扫"完成支付。

- 适用场景：PC 网站支付、实体店单品或订单支付、媒体广告支付、无人售卖机等。

## 协议授权支付（PAYANDSIGN）

商户提前与用户签订支付协议（如三方代扣协议），得到用户授权令牌。

- 用户在商户网站购买商品时，商户使用授权令牌直接从用户账户扣款。

## 现金充值支付（CASHTOPUP）

商户线上请求 PayBy 收单接口下单，用户通过线下支持现金充值的门店完成支付。

## 直联支付（DIRECTPAY）

商户收集用户的支付卡信息后，通过 API 方式直接发起支付。

- 支持 DevicePay。
- 支持分期（installment）等场景参数。

## 相关链接

- 业务域总览：[[domain_payby_merchant_payment_api]]
- 接口与字段：[[payby-merchant-api-overview]]
