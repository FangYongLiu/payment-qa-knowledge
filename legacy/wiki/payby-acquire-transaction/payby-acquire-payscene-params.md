---
title: PayBy交易场景参数关系(paySceneParams)
domain: acquire-transaction
kind: wiki_page
slug: payby-acquire-payscene-params
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:1d3b3713-3d92-4fd2-a760-42f5f4e3a4b6
tags: []
---

# PayBy交易场景参数关系(paySceneParams)

本页汇总各 `paySceneCode` 对应的 `paySceneParams` 与 `interactionParams` 字段清单，并解释字段含义。支付场景的业务说明见 [[payby-acquire-payment-scenarios]]，协议与通用参数规则见 [[payby-acquire-protocol-rules]]，相关订单字段见 [[payby-acquire-data-models]]。

## 场景参数对照表

| PayScene | paySceneParams | interactionParams |
| --- | --- | --- |
| JSAPI | payerMid (可填)<br/>oneTimePayment (可填) | tokenUrl |
| INAPP | iapDeviceId (必填)<br/>appId (必填) | tokenUrl |
| PAYPAGE | redirectUrl (可填)<br/>oneTimePayment (可填)<br/>customerId (可填)<br/>changePayer (可填) | tokenUrl |
| DYNQR | oneTimePayment (可填)<br/>changePayer (可填) | tokenUrl |
| QRPAY | authCode (必填) | — |
| AUTODEBIT | authProtocolNo (必填) | — |
| CASHTOPUP | businessType (必填) | tokenUrl |
| FACE | authToken (必填)<br/>uniqueDevice (必填) | — |
| DIRECTPAY | 见下文「DIRECTPAY 三种子模式」 | threeDSecureDom / installmentUrl(分期) |
| EWALLET | redirectUrl (可填)<br/>oneTimePayment (可填)<br/>eWalletCode | deepLink |
| PAYANDSIGN | protocolSceneCode (必填)<br/>protocolNotifyUrl (可填)<br/>customerId (可填) | tokenUrl |

## DIRECTPAY 子模式参数

DIRECTPAY 按场景使用不同参数集。

### 首次支付（卡支付）
- cardNo (必填)：持卡人卡号 PAN，加密传输
- holderName (必填)：持卡人姓名，加密传输
- cvv (必填)：卡片安全码 CVV/CVC/CVN/CVE/CID，加密传输
- expYear (必填) / expMonth (必填)：失效年/月
- email (可填)：持卡人联系邮箱
- platformType (必填)：交易平台，如 H5、WEB、iOS、Android
- threeDSecure (选填)：是否强制 3DS 验证；PayBy 风控判定优先于商户要求
- customerId (必填)：付款人在商户处唯一标识，用于 PayBy 静默开户标记
- realIP (必填)：交易发生时真实 IP
- saveCard (必填)：是否保存银行卡用于后续交易
- redirectUrl (必填)

### savedCard 支付
- cardToken (必填)：首次支付返回的 savedCard 标识；同传 cardNo 时 cardNo 不生效
- cvv (必填)
- email (可填)
- platformType (必填)
- threeDSecure (选填)
- realIP (必填)
- redirectUrl (必填)

### 分期支付
- type (可填)：directpay 类型，可选 `BANK_CARD`、`INSTALLMENT`，默认 `BANK_CARD`
- uniqueId (必填)：分期支付 uniqueId
- redirectUrl (可填)
- platformType (必填)
- realIP (必填)
- interactionParams 返回 `installmentUrl`：分期签约 URL

## 通用 paySceneParams 字段说明

- payerMid：付款方 PayBy 会员 ID，可通过 OAuth 获取
- redirectUrl：商户网站地址，订单支付成功后重定向
- oneTimePayment：默认为 false；为 true 时订单只允许支付一次，失败即置失败
- customerId：付款人在商户处的唯一标识；PAYANDSIGN 中用于标记付款人在 PayBy 的签约方
- changePayer：是否允许更换付款人
- iapDeviceId / appId：INAPP 必填
- authCode：QRPAY 用户付款码
- authProtocolNo：AUTODEBIT 授权协议号
- authToken / uniqueDevice：FACE 授权 token 与唯一设备号，详见 Face 接口文档
- businessType：CASHTOPUP 业务类型，目前枚举：
  - `GAME_TOP_UP`：游戏充值
- protocolSceneCode：PAYANDSIGN 用户需签约的协议场景代码
- protocolNotifyUrl：协议签约通知地址

## eWalletCode 枚举（EWALLET 场景）

| code | description |
| --- | --- |
| payby | PayBy wallet |
| botim-pay | Botim wallet |
| ALIPAYPLUS | Alipay plus Wallet |
| WECHATPAY | Wechatpay Wallet（需安装 WECHAT SDK） |

## interactionParams 字段说明

- tokenUrl：包含 Token 的 URL 链接，商户系统可用 token 或完整 URL 呼起 PayBy 完成支付；有效期 1 小时，过期需用相同业务参数重新创建订单获取新 tokenUrl
- threeDSecureDom：DIRECTPAY 卡支付的 3DS 验证页
- installmentUrl：DIRECTPAY 分期签约 URL
- deepLink：EWALLET 拉起目标支付 App 的 DeepLink

## 相关入口

- 接口总览：[[payby-acquire-transaction-overview]]
- 域汇总：[[domain_payby_acquire_transaction]]
