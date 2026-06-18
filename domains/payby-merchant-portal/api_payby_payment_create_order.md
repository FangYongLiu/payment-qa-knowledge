---
id: api_payby_payment_create_order
object_type: API
domain: payby-merchant-portal
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p5
tags:
- payment
- create-order
- payby
subdomain: null
module: null
sensitivity: normal
name: PayBy创建支付订单接口
aliases: []
related_services: []
related_tables: []
related_scenarios:
- payby-payment-api-pay-scene
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
PayBy 统一支付下单接口，用于创建支付订单。支持多种交易场景：JSAPI、INAPP、PAYPAGE、DYNQR、QRPAY、AUTODEBIT、CASHTOPUP、FACE、DIRECTPAY、EWALLET、PAYANDSIGN、PREAUTH、PREAUTHVOID、CAPTURE 等。商户根据不同 paySceneCode 传入对应的 paySceneParams，PayBy 返回 interactionParams 用于完成后续支付交互（如 tokenUrl、deepLink、threeDSecureDom、installmentUrl、paymentData 等）。

## 路径/方法
原文未提供具体 URL 路径与 HTTP 方法。

## 入参
### 通用请求参数规定
- 请求参数值为空时，不予处理。

### 关键业务参数
- `paySceneCode`：交易场景代码（必填）。取值见下表。
- `currency`：货币类型，例如 `AED`（阿联酋货币单位）。
- `merchantOrderNo`：商户支付订单号（原文截断未完整给出生成规则）。
- `paySceneParams`：随 paySceneCode 变化的参数集合。
- `interactionParams`：返回的交互参数集合（出参侧）。

### 交易场景代码（paySceneCode）
| PaySceneCode | 说明 |
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

### 各场景 paySceneParams（详细对应关系参见 [[payby-payment-api-pay-scene]]）
- JSAPI：`payerMid`(可填)、`oneTimePayment`(可填)
- INAPP：`iapDeviceId`(必填)、`appId`(必填)
- PAYPAGE：`redirectUrl`(可填)、`oneTimePayment`(可填)、`customerId`(可填)、`changePayer`(可填)
- DYNQR：`oneTimePayment`(可填)、`changePayer`(可填)
- QRPAY：`authCode`(必填)
- AUTODEBIT：`authProtocolNo`(必填)
- CASHTOPUP：`businessType`(必填)，例如 `GAME_TOP_UP`（游戏充值）
- FACE：`authToken`(必填)、`uniqueDevice`(必填)
- DIRECTPAY：
  - 首次支付：`cardNo`、`holderName`、`cvv`、`expYear`、`expMonth`、`platformType`、`customerId`、`realIP`、`saveCard`、`redirectUrl`(必填)，`email`、`threeDSecure`(选填)
  - savedCard 支付：`cardToken`、`cvv`、`platformType`、`realIP`、`redirectUrl`(必填)，`email`、`threeDSecure`(选填)
  - 分期支付：`uniqueId`、`platformType`、`realIP`(必填)，`type`、`redirectUrl`(可填)
  - devicePay：`type`、`devicePayType`、`cardNum`、`cardExpYear`、`cardExpMonth`、`cryptoFmt`、`payCrypt`、`platformType`、`customerId`、`realIP`、`redirectUrl`(必填)，`holderName`、`eci`、`email`(可填)
- EWALLET：`redirectUrl`(可填)、`oneTimePayment`(可填)、`eWalletCode`、`osType`、`terminalType`、`subEWalletCode`、`openId`
- PAYANDSIGN：`protocolSceneCode`(必填)、`protocolNotifyUrl`(可填)、`customerId`(可填)
- PREAUTH：
  - 首次支付：`cardNo`、`holderName`、`cvv`、`expYear`、`expMonth`、`platformType`、`customerId`、`realIP`、`redirectUrl`(必填)，`email`(可填)
  - savedCard 支付：`cardToken`、`cvv`、`platformType`、`realIP`、`redirectUrl`(必填)，`email`(可填)
  - devicePay：`type`、`devicePayType`、`cardNum`、`cardExpYear`、`cardExpMonth`、`cryptoFmt`、`payCrypt`、`platformType`、`customerId`、`realIP`、`redirectUrl`(必填)，`holderName`、`eci`、`email`(可填)
- PREAUTHVOID：`preauthOrderNo`(必填)
- CAPTURE：`preauthOrderNo`(必填)

### 关键字段说明
- `payerMid`：付款方 PayBy 会员 ID（OAuth 获取）。
- `redirectUrl`：商户网站地址，订单支付成功后重定向。
- `oneTimePayment`：默认 false；为 true 时订单只允许支付一次，失败即置失败。
- `businessType`：例如 `GAME_TOP_UP`。
- `authToken` / `uniqueDevice`：FacePay 授权 token 与唯一授权设备号。
- `cardNo`/`holderName`/`cvv`/`cardNum`/`cardExpYear`/`cardExpMonth`/`payCrypt`：加密传输。
- `expYear`/`expMonth`：失效年/月，例 21 / 05。
- `platformType`：H5、WEB、iOS、Android。
- `threeDSecure`：商户是否强制 3DS；风控判断结果优先于商户要求。
- `customerId`：付款人在商户处的唯一标识，用于 PayBy 静默开户标记，单次支付也需上报。
- `realIP`：交易发生时真实 IP。
- `saveCard`：保存银行卡，默认 false；保存后返回卡 id，可用于 cardToken。
- `cardToken`：使用 savedCard 发起支付；与 `cardNo` 同传时 `cardNo` 不生效。
- `terminalType`：WEB/WAP/APP/MP；`eWalletCode=ALIPAYPLUS` 必填；微信小程序支付必填 `MP`。
- `osType`：IOS/ANDROID；`eWalletCode=ALIPAYPLUS` 必填。
- `subEWalletCode`：`eWallet
