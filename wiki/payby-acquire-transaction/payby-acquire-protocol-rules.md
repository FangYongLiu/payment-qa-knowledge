---
title: PayBy收单接口协议与参数规则
domain: payby-acquire-transaction
kind: wiki_page
slug: payby-acquire-protocol-rules
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:1d3b3713-3d92-4fd2-a760-42f5f4e3a4b6
tags: []
---

# PayBy收单接口协议与参数规则

本页规定商户接入 PayBy 收单接口时必须遵守的通信协议、签名要求、请求参数处理规则、交易场景代码、商户订单号生成规则及货币类型枚举。其他相关内容见 [[payby-acquire-transaction-overview]]、[[payby-acquire-payscene-params]]、[[payby-acquire-data-models]]。

## 协议规则

调用 PayBy API 必须遵守以下传输与编码约定：

| 方式 | 说明 |
| --- | --- |
| 传输方式 | 为保证交易安全，采用 HTTPS 传输 |
| 提交方式 | 采用 POST 方法提交 |
| 数据格式 | JSON |
| 字符编码 | 统一采用 UTF-8 字符编码 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应数据都需要签名 |

## 请求参数规定

- 如果请求参数的值为空，则不予处理。

## 交易场景代码 paySceneCode

| paySceneCode | 说明 |
| --- | --- |
| JSAPI | JSAPI 支付 |
| INAPP | App 支付 |
| PAYPAGE | 支付网页支付 |
| DYNQR | 动态码支付 |
| QRPAY | 付款码支付 |
| AUTODEBIT | 协议授权支付 |
| CASHTOPUP | 现金充值支付 |
| FACE | 人脸支付 |
| DIRECTPAY | 直联支付 |
| EWALLET | 电子钱包支付 |
| PAYANDSIGN | 支付并签约 |

各场景的业务说明见 [[payby-acquire-payment-scenarios]]；与之配套的 paySceneParams 与 interactionParams 的字段约束见 [[payby-acquire-payscene-params]]。

## 商户订单号 merchantOrderNo

- 由商户自定义生成。
- 仅支持使用字母、数字、中划线 `-`、下划线 `_` 这些英文半角字符的组合。
- 必须保持唯一性（建议根据当前系统时间加随机序列生成）。
- 重新发起一笔支付要使用原订单号，避免重复支付。
- 已支付过或已调用取消交易的订单号不能重新发起支付。
- 长度上限为 64 位（接口请求参数 merchantOrderNo 长度规定为 32 位，详见各接口字段定义）。

## 货币类型 currency

| currency | 说明 |
| --- | --- |
| AED | 阿联酋货币单位 |

货币类型作为 `Money` 数据结构的一部分使用，详见 [[payby-acquire-data-models]]。
