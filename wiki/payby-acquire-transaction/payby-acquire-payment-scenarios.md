---
title: PayBy支付场景说明
domain: payby-acquire-transaction
kind: wiki_page
slug: payby-acquire-payment-scenarios
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:1d3b3713-3d92-4fd2-a760-42f5f4e3a4b6
tags: []
---

# PayBy支付场景说明

本页详细说明 PayBy 收单系统支持的各类支付场景（paySceneCode）的业务定义、适用环境，以及商户对应的呼起/调用方式。各场景所需的 `paySceneParams` 与 `interactionParams` 参数关系详见 [[payby-acquire-payscene-params]]。

## 支付场景代码总览(paySceneCode)

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
| PAYANDSIGN | 支付并签约 |

## JSAPI 支付

- 业务定义：商户已有 H5 商城网站，用户在 PayBy 内访问该网站时，可调用 PayBy 完成下单购买。
- 调用方式：在 PayBy App 内通过 `ToPayJSBridge` 呼起支付，传入 `appId`(partnerId) 和 `token`。
- 关键流程：
  - 监听 `ToPayJSBridgeReady`，调用 `window.ToPayJSBridge.init`。
  - 调用 `window.ToPayJSBridge.invoke('ToPayRequest', {appId, token}, callback)`。
  - 回调中 `res.status === 'success'` 即为支付成功。

```javascript
function onBridgeReady() {
  window.ToPayJSBridge.init(function(message, responseCallback) {})
}
if (typeof ToPayJSBridge === 'undefined') {
  document.addEventListener('ToPayJSBridgeReady', onBridgeReady, false)
} else {
  onBridgeReady()
}
window.ToPayJSBridge.invoke('ToPayRequest',
  { appId: 'xx', token: token },
  function(data) {
    const res = JSON.parse(data)
    if (res.status === 'success') { /* Success Callback */ }
  }
)
```

## INAPP 支付（App支付）

- 业务定义：移动端支付。商户在自有移动端 App 中集成 PayBy 开放 SDK，调起 PayBy 模块完成支付。
- 调用方式：商户将 `interactionParams` 中的 `token` 传入 PayBy SDK，呼起 PayBy 等支付 App 完成支付。
- 必填场景参数：`iapDeviceId`、`appId`。

## PAYPAGE 支付（支付网页支付）

- 业务定义：在手机、iPad、电脑等设备的浏览器中跳转到 PayBy 支付网页完成支付。
- 调用方式：通过重定向或 `openwindow` 让用户用浏览器打开 `interactionParams` 中的 `tokenUrl`，在 PayBy 收银台页面选择支付方式完成支付。
- 可填场景参数：`redirectUrl`、`oneTimePayment`、`customerId`、`changePayer`。

## DYNQR 支付（动态码支付）

- 业务定义：商户按 PayBy 协议生成支付二维码，用户用 PayBy 扫一扫完成支付。
- 适用场景：PC 网站支付、实体店单品/订单支付、媒体广告支付、无人售卖机等。
- 调用方式：商户将 `interactionParams.tokenUrl` 转换为二维码，用户用 PayBy App 扫码支付。

## QRPAY 支付（付款码支付）

- 业务定义：用户出示 PayBy 内的"付款码"给商户系统扫描后直接完成支付。
- 适用场景：线下面对面收银。
- 调用方式：商户通过扫码枪、POS 等设备扫描用户付款二维码，将付款二维码数据作为 `authCode`（必填）提交完成扣款。

## AUTODEBIT 支付（协议授权支付）

- 业务定义：商户提前与用户签订支付协议（如三方代扣协议），获得授权令牌；后续用户在商户网站消费时，商户可凭授权令牌从用户账户直接扣款。
- 调用方式：使用用户绑定的 PayBy 授权协议号 `authProtocolNo`（必填）发起支付。

## CASHTOPUP 支付（现金充值支付）

- 业务定义：商户线上请求 PayBy 收单接口下单，用户线下到支持现金充值的门店完成支付。
- 调用方式：线上接口创建订单，客户线下支付现金完成支付。
- 必填场景参数：`businessType`，当前枚举：
  - `GAME_TOP_UP`：游戏充值。

## FACE 支付（人脸支付）

- 业务定义：使用 PayBy FacePay 完成支付。
- 必填场景参数：
  - `authToken`：FacePay 授权 token（获取方式见 Face 接口文档）。
  - `uniqueDevice`：FacePay 唯一授权设备号（获取方式见 Face 接口文档）。

## DIRECTPAY 支付（直联支付）

- 业务定义：商户收集用户支付卡信息后，通过 API 提交给 PayBy 完成支付。
- 三种子场景的参数差异详见 [[payby-acquire-payscene-params]]：
  - 首次支付：`cardNo`、`holderName`、`cvv`、`expYear`、`expMonth`、`platformType`、`customerId`、`realIP`、`saveCard`、`redirectUrl` 必填；`email`、`threeDSecure` 可填。
  - savedCard 支付：使用首次支付返回的 `cardToken` + `cvv` 等支付；`cardNo` 与 `cardToken` 同传时以 `cardToken` 为准。
  - 分期支付：`uniqueId`、`platformType`、`realIP` 必填，`type`、`redirectUrl` 可填。
- 关键参数说明：
  - `cardNo` / `holderName` / `cvv`：加密传输。
  - `threeDSecure`：商户是否强制 3DS；最终是否触发以 PayBy 风控为准。
  - `customerId`：付款人在商户处的唯一标识，用于 PayBy 静默开户标记，单次支付也需上报。
  - `saveCard`：是否保存卡信息以便复用，返回 `savedCard` 卡 id。
  - `type`：directpay 类型，可选 `BANK_CARD`、`INSTALLMENT`，默认 `BANK_CARD`。
- 交互参数：
  - 普通流程：`threeDSecureDom`。
  - 分期支付：`installmentUrl`（分期签约 URL）。

## EWALLET 支付（电子钱包支付）

- 业务定义：商户在自有页面下单并选定支付 App 后，PayBy 直接返回移动应用拉起方式，降低移动支付接入门槛。
- 适用对象：需要将支付软件作为支付渠道补充、且对网页控制要求高的商户。
- 场景参数：`redirectUrl`（可填）、`oneTimePayment`（
