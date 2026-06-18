---
title: 支付场景码PaySceneCode说明
domain: acquire-transaction
kind: wiki_page
slug: acquire-pay-scene-code
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997851554
tags: []
---

# 支付场景码PaySceneCode说明

`PaySceneCode` 用于标识收单交易中的具体支付场景，在 SGS 接口及下游服务间传递时区分不同的支付方式与受理形态。

## 场景码列表

| PaySceneCode | 说明 |
| --- | --- |
| JSAPI | JSAPI⽀付 |
| INAPP | App⽀付 |
| PAYPAGE | ⽀付⽹⻚⽀付 |
| DYNQR | 动态码⽀付 |
| QRPAY | 付款码⽀付 |
| AUTODEBIT | 协议授权⽀付 |
| CASHTOPUP | 现⾦充值⽀付 |
| FACE | ⼈脸⽀付 |
| DIRECTPAY | 直联⽀付 |
| EWALLET | 电⼦钱包⽀付 |
| PAYANDSIGN | PAYANDSIGN |

## 相关参考

- 支付渠道维度的取值参见 [[acquire-pay-channel-no]]
- 业务域整体说明见 [[acquire-transaction-overview]]
