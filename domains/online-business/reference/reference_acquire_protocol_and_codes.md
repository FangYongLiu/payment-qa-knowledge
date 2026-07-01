---
id: reference_acquire_protocol_and_codes
object_type: Reference
name: 收单接入协议 / 支付场景码 / 渠道号 速查
aliases: [PaySceneCode, PayChannelNo, paySceneParams, SGS协议规则]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/997851554 + PayBy API v2.25 + wiki:725ad723
tags: [online-business, acquiring, SGS, paySceneCode, payChannelNo]
related_services: [svc_sgs, svc_acquireii]
---

# 收单接入协议 / 支付场景码 / 渠道号 速查

> SGS 收单接入的通用规则 + 两类核心枚举(PaySceneCode / PayChannelNo)+ 各场景的 paySceneParams/interactionParams 字段关系。
> 来源:Confluence 收单业务域 + PayBy 接口文档 v2.25。QA 写/测收单用例的字典。

## 接入协议规则(SGS API 通用)

| 方式 | 约定 |
| --- | --- |
| 传输方式 | HTTPS |
| 提交方式 | POST |
| 数据格式 | JSON |
| 字符编码 | UTF-8 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求与响应数据都需签名(Header `Sign`) |
| 请求参数 | 值为空的参数不予处理 |

**公共 Http Header**:`Content-Language`(可选,如 `en`)、`Sign`(必填)、`Partner-Id`(必填,商户号 String(12))。
**公共 Http Body**:`requestTime`(必填,Timestamp(3) 毫秒)、`bizContent`(必填,各接口对应请求对象)。
**公共响应**:Body 含 `head`(ResponseHeader:`applyStatus`/`code`/`msg`/`success`/`traceCode`)与可选 `body`;**`body` 仅在 `applyStatus=SUCCESS` 且 `code=0` 时返回**。
**环境**:联调 `https://uat.test2pay.com`,生产 `https://api.payby.com`。

### 通用返回码(收单/会员类共用)
| code | msg | 含义 |
| --- | --- | --- |
| 0 | SUCCESS | 成功 |
| 400 | INVALID_PARAMETER | 参数错误 |
| 400 | REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER | 请求时间过早/过晚 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 |
| 403 | UNAUTHORIZED | API 未授权 |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 |
| 500 | SYSTEM_ERROR | 系统错误 |
| 504 | SERVICE_TIMEOUT | 服务超时 |
| 601 | RISK_FAIL | 风控校验失败 |

### 商户订单号 merchantOrderNo 规则
- 商户自定义,仅字母/数字/中划线 `-`/下划线 `_`;须唯一(建议时间戳+随机序列)。
- 重发同一笔支付须用原订单号;**已支付或已取消的订单号不可复用**。
- 长度上限 64 位(部分接口请求字段定义为 32 位,以各接口字段定义为准)。

### 货币类型 currency
- `AED` — 阿联酋迪拉姆。`Money` 结构 = `{currency, amount(Decimal(12,2))}`,示例 `{"currency":"AED","amount":123.45}`。

## 支付场景码 PaySceneCode

| PaySceneCode | 说明 |
| --- | --- |
| JSAPI | JSAPI 支付(PayBy 内 H5 商城,`ToPayJSBridge` 呼起) |
| INAPP | App 支付(商户 App 集成 PayBy SDK) |
| PAYPAGE | 支付网页支付(浏览器跳 PayBy 收银台) |
| DYNQR | 动态码支付(商户生成二维码,用户 PayBy 扫) |
| QRPAY | 付款码支付(用户出示付款码,商户扫) |
| AUTODEBIT | 协议授权支付(凭 authProtocolNo 代扣) |
| CASHTOPUP | 现金充值支付(线上下单,线下门店现金) |
| FACE | 人脸支付(FacePay) |
| DIRECTPAY | 直联支付(商户收集卡信息经 API 提交) |
| EWALLET | 电子钱包支付(返回拉起目标钱包的 DeepLink) |
| PAYANDSIGN | 支付并签约 |

## 支付渠道号 PayChannelNo

| PayChannelNo | Description |
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

## 各场景 paySceneParams / interactionParams 对照

| PayScene | paySceneParams | interactionParams |
| --- | --- | --- |
| JSAPI | payerMid(可) / oneTimePayment(可) | tokenUrl |
| INAPP | iapDeviceId(必) / appId(必) | tokenUrl |
| PAYPAGE | redirectUrl / oneTimePayment / customerId / changePayer(均可) | tokenUrl |
| DYNQR | oneTimePayment / changePayer(可) | tokenUrl |
| QRPAY | authCode(必) | — |
| AUTODEBIT | authProtocolNo(必) | — |
| CASHTOPUP | businessType(必,目前枚举 `GAME_TOP_UP`) | tokenUrl |
| FACE | authToken(必) / uniqueDevice(必) | — |
| DIRECTPAY | 见下「DIRECTPAY 子模式」 | threeDSecureDom / installmentUrl(分期) |
| EWALLET | redirectUrl / oneTimePayment(可) / eWalletCode | deepLink |
| PAYANDSIGN | protocolSceneCode(必) / protocolNotifyUrl(可) / customerId(可) | tokenUrl |

### DIRECTPAY 子模式参数
- **首次支付(卡支付)**:`cardNo`/`holderName`/`cvv`(均加密,必填)、`expYear`/`expMonth`(必)、`platformType`(必,如 H5/WEB/iOS/Android)、`customerId`(必,商户侧付款人唯一标识,用于 PayBy 静默开户)、`realIP`(必)、`saveCard`(必)、`redirectUrl`(必);`email`/`threeDSecure` 可填。
- **savedCard 支付**:`cardToken`(必,首次支付返回)+ `cvv`(必)+ `platformType`/`realIP`/`redirectUrl`(必);`cardNo` 与 `cardToken` 同传时**以 cardToken 为准**。
- **分期支付**:`uniqueId`(必)、`platformType`(必)、`realIP`(必);`type`(可,`BANK_CARD`/`INSTALLMENT`,默认 `BANK_CARD`)、`redirectUrl`(可);interactionParams 返回 `installmentUrl`(分期签约 URL)。

### 通用字段说明
- `threeDSecure`:商户是否强制 3DS;**最终是否触发以 PayBy 风控为准**。
- `oneTimePayment`:默认 false;true 时订单只允许支付一次,失败即置失败。
- `tokenUrl`:含 Token 的 URL,**有效期 1 小时**,过期需以相同业务参数重建订单取新 tokenUrl。
- `eWalletCode` 枚举(EWALLET):`payby` / `botim-pay` / `ALIPAYPLUS` / `WECHATPAY`(需装 WECHAT SDK)。

## eWalletCode 与场景细节(补充)
- JSAPI:监听 `ToPayJSBridgeReady` → `ToPayJSBridge.init` → `invoke('ToPayRequest', {appId, token}, cb)`,回调 `res.status==='success'` 即成功。
- QRPAY:商户扫码枪/POS 扫用户付款码,付款码数据作为 `authCode` 提交扣款。
- AUTODEBIT:凭用户绑定的授权协议号 `authProtocolNo` 发起。

## 关联关系
- **接入网关**:[[svc_sgs]](= `related_services`),收单核心 [[svc_acquireii]]。
- **配套接口**:见 [[api_sgs_acquire_place_order]] 等收单 API 对象。
- **场景参数落库**:[[tbl_acquireii_t_pay_scene_param]] 支付场景参数表(由该表的 `related_services` 反指)。

## QA 关注点
- PaySceneCode × PayChannelNo 的组合覆盖与匹配验证。
- DIRECTPAY 三种子模式(首次/savedCard/分期)的必填参数差异;加密字段(cardNo/holderName/cvv)。
- tokenUrl 1 小时过期边界;merchantOrderNo 唯一性与不可复用。
- 各场景 interactionParams 是否按预期返回(如 DIRECTPAY 返回 threeDSecureDom / installmentUrl)。
