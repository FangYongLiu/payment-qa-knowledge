---
title: PayBy授权协议签约返回码总览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-auth-protocol-return-codes
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p10
tags: []
---

# PayBy授权协议签约返回码总览

本页汇总 PayBy 授权协议签约相关接口（[[api_payby_apply_protocol]]、[[api_payby_get_protocol]]）的全部返回码、含义、原因及推荐解决方案，便于排错和对接联调时统一查阅。返回码通过响应体 `head.code` 与 `head.msg` 字段返回，业务是否成功还需结合 `head.applyStatus`（`SUCCESS`/`FAIL`/`ERROR`）综合判断。

相关页面：[[payby-auth-protocol-overview]]、[[api_payby_protocol_notify]]。

## 通用返回码（公共错误）

适用于所有签约相关 API。

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 0    | SUCCESS               | 成功                     |                     |
| 400  | INVALID_PARAMETER     | 参数错误                 | 调整请求参数        |
| 400  | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间        |
| 400  | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间        |
| 402  | RATE_LIMIT_REJECT     | 请求过于频繁             | 降低请求频率        |
| 403  | UNAUTHORIZED          | API 未授权               | 联系 PayBy          |
| 404  | SERVICE_NOT_AVAILABLE | API 服务不可用           | 联系 PayBy          |
| 500  | SYSTEM_ERROR          | 系统错误                 | 联系 PayBy，稍后重试 |
| 504  | SERVICE_TIMEOUT       | 服务超时                 | 稍后重试            |
| 601  | RISK_FAIL             | 风控校验失败             | 请调整业务          |

## 申请签约协议专属返回码

适用于 [[api_payby_apply_protocol]]（`/sgs/api/protocol/applyProtocol`）。

| code  | msg | 原因 | 解决方案 |
| ----- | --- | ---- | -------- |
| 90001 | MISSING_IAP_DEVICE_ID             | 缺少 deviceId            | 调整请求参数 |
| 90002 | MISSING_APP_ID                    | 缺少 appId               | 调整请求参数 |
| 90003 | INVALID_APP_ID                    | 无效的 appId             | 调整请求参数 |
| 90004 | INVALID_LANG_TYPE                 | 无效的语言类型           | 调整请求参数 |
| 90006 | INVALID_PROTOCOL_SCENE_CODE       | 无效的 protocolSceneCode | 调整场景代码 |
| 90007 | EXPIREDTIME_ILLEGAL               | 过期时间非法             | 调整过期时间 |
| 90008 | EXPIREDTIME_LESS_THAN_REQUESTTIME | 过期时间小于请求时间     | 调整过期时间 |
| 90009 | INVALID_ACCESS_TYPE               | 无效的 accessType        | 调整请求参数 |

提示：
- `90001`、`90002` 通常出现在 `accessType=SDK` 场景下未填写 `protocolSceneParams.iapDeviceId` 或 `appId`。
- `90009` 为 v1.0.1 新增，校验 `accessType` 必须为 `SDK` 或 `H5`。

## 查询协议专属返回码

适用于 [[api_payby_get_protocol]]（`/sgs/api/protocol/getProtocol`）。

| code  | msg | 原因 | 解决方案 |
| ----- | --- | ---- | -------- |
| 90005 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |

## 卡支付/通用业务参数返回码（62xxx 段）

下表为签约/支付链路中卡相关与通用业务参数校验错误码，多见于卡信息、邮箱、IP、协议场景、分账等参数缺失或非法时。

| code  | msg | 原因 | 解决方案 |
| ----- | --- | ---- | -------- |
| 62054 | MISSING_EXP_MONTH                 | 缺少 expMonth                                  | 调整请求参数 |
| 62055 | MISSING_CUSTOMER_ID               | 缺少 customerId                                | 调整请求参数 |
| 62056 | MISSING_EMAIL                     | 缺少 email                                     | 调整请求参数 |
| 62057 | INVALID_SAVE_CARD                 | 无效的 saveCard                                | 调整请求参数 |
| 62058 | INVALID_THREEDSECURE              | 无效的 threeDSecure                            | 调整请求参数 |
| 62059 | INVALID_EMAIL                     | 无效的 email                                   | 调整请求参数 |
| 62060 | INVALID_PLATFORM_TYPE             | 无效的 platformType                            | 调整请求参数 |
| 62061 | MISSING_REAL_IP                   | 缺少 realIP                                    | 调整请求参数 |
| 62062 | INVALID_REAL_IP                   | 无效的 realIP                                  | 调整请求参数 |
| 62063 | INVALID_EXP_YEAR                  | 无效的 expYear                                 | 调整请求参数 |
| 62064 | INVALID_EXP_MONTH                 | 无效的 expMonth                                | 调整请求参数 |
| 62065 | INVALID_CARD_NO                   | 无效的 cardNo                                  | 调整请求参数 |
| 62066 | INVALID_CVV                       | 无效的 cvv                                     | 调整请求参数 |
| 62067 | HOLDER_NAME_TOO_LONG              | holderName 超长                                | 调整请求参数 |
| 62068 | MISSING_SAVE_CARD                 | 缺少 saveCard                                  | 调整请求参数 |
| 62069 | CARD_NO_LENGTH_UNMATCH            | cardNo 长度不匹配                              | 调整请求参数 |
| 62070 | CARD_BIN_NOT_SUPPORTED            | cardBin 不支持                                 | 调整请求参数 |
| 62071 | CARD_BIN_UNAVAILABLE              | cardBin 不可用                                 | 调整请求参数 |
| 62072 | MISSING_REDIRECT_URL              | 缺少 redirectUrl                               | 调整请求参数 |
| 62073 | INVALID_ONE_TIME_PAYMENT          | 无效的 oneTimePayment                          | 调整请求参数 |
| 62078 | CARD_NOT_EXIST                    | cardToken 填写错误或者卡已解绑                 | 调整请求参数 |
| 62079 | MISSING_CARD_NO_CARD_TOKEN        | cardToken 和 cardNo 同时为空                   | 调整请求参数 |
| 62080 | MISSING_EWALLET_CODE              | 缺少 eWalletCode                               | 调整请求参数 |
| 62081 | INVAL
