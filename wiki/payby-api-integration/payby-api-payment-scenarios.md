---
title: PayBy支付场景术语
domain: payby-open-api
kind: wiki_page
slug: payby-api-payment-scenarios
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p4
tags: []
---

# PayBy支付场景术语

本页梳理 PayBy 支持的各类支付场景定义，便于在接入前快速判断业务模式与适用范围。接口调用规范见 [[payby-api-protocol-rules]]。

## JSAPI支付

- 适用商户已有 H5 商城网站。
- 用户在 PayBy 内访问该 H5 站点时，调用 PayBy 完成下单购买。

## App支付

- 又称移动端支付。
- 商户在移动端应用 APP 中集成开放 SDK，拉起 PayBy 模块完成支付。

## 支付网页支付

- 在手机、ipad、电脑等设备中，通过浏览器跳转到 PayBy 支付网页完成支付。

## 付款码支付

- 用户展示 PayBy 内的"付款码"，由商户系统扫描后直接完成支付。
- 主要应用于线下面对面收银场景。

## 动态码支付

- 商户系统按 PayBy 协议生成支付二维码，用户使用 PayBy "扫一扫"完成支付。
- 适用场景：PC 网站支付、实体店单品或订单支付、媒体广告支付、无人售卖机等。

## 协议授权支付

- 商户提前与用户签订支付协议（如三方代扣协议），取得用户授权令牌。
- 用户后续在商户网站购物时，商户使用授权令牌直接从用户账户扣款。

## 现金充值支付

- 商户线上调用 PayBy 收单接口下单。
- 用户通过线下支持现金充值的门店完成支付。

## 直联支付

- 商户收集用户的支付卡信息后，通过 API 方式提交给 PayBy 请求完成支付。

## 电子钱包支付

- 商户在自有页面完成下单并选定支付 APP 后，直接返回移动应用拉起方式。
- 进一步降低商户接入移动支付应用的开发门槛。
- 适用：需要使用支付软件作为支付渠道补充、且对网页控制要求较高的商户群体。

## 支付并签约

（原文未提供具体说明）

## 相关名词

- **PayBy支付系统**：指完成 PayBy 支付流程中涉及的 API 接口、后台业务处理系统、回调通知等系统的总称。
