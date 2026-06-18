---
title: PayBy支付场景码与支付渠道号
domain: payby-acquire-transaction
kind: wiki_page
slug: payby-acquire-pay-scene-codes
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:725ad723-2e21-421d-837b-1ac7e8e0fd3a
tags: []
---

# PayBy支付场景码与支付渠道号

本页汇总 PayBy 收单交易中使用的两类核心枚举：用于标识支付场景的 `PaySceneCode`，以及用于标识资金渠道的 `PayChannelNo`。完整的业务上下文见 [[payby-acquire-transaction-overview]]。

## 支付场景码 PaySceneCode

用于标识发起支付时所处的业务场景。

| PaySceneCode | 说明 |
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
| PAYANDSIGN | PAYANDSIGN |

## 支付渠道号 PayChannelNo

用于标识完成资金扣款/收款所使用的渠道。

| Pay Channel No | Description |
| --- | --- |
| 04 | 对私网银 |
| 12 | 对公网银 |
| 14 | 余额 |
| 15 | 快捷支付 |
| 16 | 线下汇款 |
| 17 | MOTO |
| 18 | KIOSK |
| 20 | PayLater |
| 21 | ALIPAY |
| 22 | GP抵扣 |
| 23 | GP支付 |
| 30 | 国际卡 |

## 相关参考

- 接入文档（SGS）：https://developers.payby.com/docs/General/integration-guide
- SGS 接口测试平台：https://qa.test2pay.com/manualTest/gateway/sgs
- 涉及的应用归属见 [[payby-acquire-applications-owners]]
- 相关数据表查询见 [[payby-acquire-databases-guide]]
