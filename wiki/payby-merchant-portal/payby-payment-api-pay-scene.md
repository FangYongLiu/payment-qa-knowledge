---
title: PayBy支付接口 - 交易场景与参数规定
domain: payby-merchant-portal
kind: wiki_page
slug: payby-payment-api-pay-scene
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p5
tags: []
---

# PayBy支付接口 - 交易场景与参数规定

本页梳理 PayBy 支付接口中 `paySceneCode` 的所有交易场景枚举、各场景下 `paySceneParams` 与 `interactionParams` 的对应关系，以及各支付方式的接入说明。具体下单接口字段见 [[api_payby_payment_create_order]]。

## 交易场景代码 (paySceneCode)

| paySceneCode | 说明 |
| --- | --- |
| JSAPI | JSAPI支付 |
| INAPP | App支付 |
| PAYPAGE | 支付网页支付 |
| DYNQR | 动态码支付 |
| QRPAY | 付款码支付 |
| AUTODEBIT | 协议授权支付 |
| CASHTOPUP | 现金充值支付 |
| FACE | 人脸支付 |
| DIRECTPAY | 直联支付 |
| EWALLET | 电子钱包支付 |
| PAYANDSIGN | PAYANDSIGN |
| PREAUTH | 预授权 |
| PREAUTHVOID | 预授权取消（未 capture 的授权交易才可以 void） |
| CAPTURE | 预授权确认 |

## 交易场景参数关系（paySceneParams 与 interactionParams）

### JSAPI
- paySceneParams：`payerMid`(可填)、`oneTimePayment`(可填)
- interactionParams：`tokenUrl`

### INAPP
- paySceneParams：`iapDeviceId`(必填)、`appId`(必填)
- interactionParams：`tokenUrl`

### PAYPAGE
- paySceneParams：`redirectUrl`(可填)、`oneTimePayment`(可填)、`customerId`(可填)、`changePayer`(可填)
- interactionParams：`tokenUrl`

### DYNQR
- paySceneParams：`oneTimePayment`(可填)、`changePayer`(可填)
- interactionParams：`tokenUrl`

### QRPAY
- paySceneParams：`authCode`(必填)
- interactionParams：无

### AUTODEBIT
- paySceneParams：`authProtocolNo`(必填)
- interactionParams：无

### CASHTOPUP
- paySceneParams：`businessType`(必填)
- interactionParams：`tokenUrl`
- businessType 取值：

| name | desc |
| --- | --- |
| GAME_TOP_UP | 游戏充值 |

### FACE
- paySceneParams：`authToken`(必填)、`uniqueDevice`(必填)
- interactionParams：无

### DIRECTPAY
按子模式区分 paySceneParams：

- 首次支付：`cardNo`、`holderName`、`cvv`、`expYear`、`expMonth`、`platformType`、`customerId`、`realIP`、`saveCard`、`redirectUrl`（均必填），`email`(可填)、`threeDSecure`(选填)
- savedCard 支付：`cardToken`、`cvv`、`platformType`、`realIP`、`redirectUrl`（必填），`email`(可填)、`threeDSecure`(选填)
- 分期支付：`uniqueId`、`platformType`、`realIP`（必填），`type`(可填)、`redirectUrl`(可填)
- devicePay：`type`、`devicePayType`、`cardNum`、`cardExpYear`、`cardExpMonth`、`cryptoFmt`、`payCrypt`、`platformType`、`customerId`、`realIP`、`redirectUrl`（必填），`holderName`、`eci`、`email`(可填)

interactionParams：
- `threeDSecureDom`
- 分期支付：`installmentUrl`

### EWALLET
- paySceneParams：`redirectUrl`(可填)、`oneTimePayment`(可填)、`eWalletCode`、`osType`、`terminalType`、`subEWalletCode`、`openId`
- interactionParams：`deepLink`(非空返回时优先使用)、`tokenUrl`、`paymentData`

### PAYANDSIGN
- paySceneParams：`protocolSceneCode`(必填)、`protocolNotifyUrl`(可填)、`customerId`(可填)
- interactionParams：`tokenUrl`

### PREAUTH
按子模式区分 paySceneParams：

- 首次支付：`cardNo`、`holderName`、`cvv`、`expYear`、`expMonth`、`platformType`、`customerId`、`realIP`、`redirectUrl`（必填），`email`(可填)
- savedCard 支付：`cardToken`、`cvv`、`platformType`、`realIP`、`redirectUrl`（必填），`email`(可填)
- devicePay：`type`、`devicePayType`、`cardNum`、`cardExpYear`、`cardExpMonth`、`cryptoFmt`、`payCrypt`、`platformType`、`customerId`、`realIP`、`redirectUrl`（必填），`holderName`、`eci`、`email`(可填)

interactionParams：`threeDSecureDom`

### PREAUTHVOID
- paySceneParams：`preauthOrderNo`(必填)

### CAPTURE
- paySceneParams：`preauthOrderNo`(必填)

## 参数说明

### 通用参数
- `payerMid`：付款方的 PayBy 会员 ID，可通过 OAuth 获取（详见 PayBy OAuth 接口文档）。
- `redirectUrl`：商户网站地址，订单支付成功后重定向到该地址。
- `tokenUrl`：包含 Token 的 URL 链接；商户系统可使用 token 或完整 URL 呼起 PayBy 完成支付；有效期 1 小时，过期需用相同业务参数重新创建订单。
- `oneTimePayment`：默认 false；为 true 时订单只允许支付一次，支付失败则订单置失败。
- `paymentData`：JSON 结构，包含 `prepay_id`、`wx_signature` 等键。

### Face 支付
- `authToken`：FacePay 授权 token（详见 Face 接口文档）。
- `uniqueDevice`：FacePay 唯一授权设备号（详见 Face 接口文档）。

### 卡支付（DIRECTPAY/PREAUTH）
- `cardNo`：持卡人卡号 (PAN)，加密传输。
- `holderName`：持卡人姓名，加密传输。
- `cvv`：银行卡 CVV/CVC/CVN/CVE/CID，加密传输。
- `expYear` / `expMonth`：失效年份 / 月份，例如 21 / 05。
- `email`：持卡人联系邮箱。
- `platformType`：交易发生平台，如 H5、WEB、iOS、Android。
- `threeDSecure`：商户是否强制要求 3DS 验证；默认 False；PayBy 风控判断结果优先于商户要求。
- `customerId`：付款人在商户处的唯一标识，用于 PayBy 静默开户标记（与 PayBy member 体系不同）；单次支付也需上报。
- `realIP`：交易发生时的真实 IP。
- `saveCard`：是否保存付款人银行卡，默认 False；保存后 PayBy 返回卡 id，下次可直接以卡 id 代替
