---
title: PayBy授权协议签约返回码总览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-auth-protocol-return-codes
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-auth-agreement-v1.0.2-p1
tags: []
---

# PayBy授权协议签约返回码总览

本页汇总 PayBy 授权协议签约相关接口（[[api_payby_apply_protocol]]、[[api_payby_get_protocol]]）的全部返回码、含义、原因及推荐解决方案，便于排错和对接联调时统一查阅。返回码通过响应体 `head.code` 与 `head.msg` 字段返回，业务是否成功还需结合 `head.applyStatus`（`SUCCESS`/`FAIL`/`ERROR`）综合判断。

相关页面：[[payby-auth-protocol-overview]]、[[api_payby_protocol_notify]]。

## 版本变更要点

- v1.0.0（2020-08-14）：初稿。
- v1.0.1（2021-10-08）：申请签约协议新增请求参数 `accessType`；调整协议场景参数关系；新增返回码 `90009`。
- v1.0.2（2022-12-30）：查询协议响应新增返回字段 `deductType`、`extension`（不影响返回码集合）。

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
- `90001`、`90002` 通常出现在 `accessType=SDK` 场景下未填写 `protocolSceneParams.iapDeviceId` 或 `appId`。在 `accessType=H5` 场景下，`protocolSceneParams` 仅含可空的 `redirectUrl`。
- `90009` 为 v1.0.1 新增，校验 `accessType` 必须为 `SDK` 或 `H5`；当请求未传 `accessType` 时默认为 `SDK`。
- `90007` / `90008` 与 `expiredTime` 有关，`expiredTime` 默认 15 分钟，不能早于 `requestTime`。

## 查询协议专属返回码

适用于 [[api_payby_get_protocol]]（`/sgs/api/protocol/getProtocol`）。

| code  | msg | 原因 | 解决方案 |
| ----- | --- | ---- | -------- |
| 90005 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |

## 全量返回码总览

下表为签约协议域汇总后的全量返回码（合并 applyProtocol 与 getProtocol）。

| code  | msg | 原因 | 解决方案 |
| ----- | --- | ---- | -------- |
| 0     | SUCCESS                           | 成功                     |                     |
| 400   | INVALID_PARAMETER                 | 参数错误                 | 调整请求参数        |
| 400   | REQUESTTIME_TOO_EARLY             | 请求时间比当前时间早太多 | 调整请求时间        |
| 400   | REQUESTTIME_TOO_LATER             | 请求时间比当前时间晚太多 | 调整请求时间        |
| 402   | RATE_LIMIT_REJECT                 | 请求过于频繁             | 降低请求频率        |
| 403   | UNAUTHORIZED                      | API 未授权               | 联系 PayBy          |
| 404   | SERVICE_NOT_AVAILABLE             | API 服务不可用           | 联系 PayBy          |
| 500   | SYSTEM_ERROR                      | 系统错误                 | 联系 PayBy，稍后重试 |
| 504   | SERVICE_TIMEOUT                   | 服务超时                 | 稍后重试            |
| 601   | RISK_FAIL                         | 风控校验失败             | 请调整业务          |
| 90001 | MISSING_IAP_DEVICE_ID             | 缺少 deviceId            | 调整请求参数        |
| 90002 | MISSING_APP_ID                    | 缺少 appId               | 调整请求参数        |
| 90003 | INVALID_APP_ID                    | 无效的 appId             | 调整请求参数        |
| 90004 | INVALID_LANG_TYPE                 | 无效的语言类型           | 调整请求参数        |
| 90005 | MERCHANT_ORDER_NO_NOT_EXIST       | 商户订单号的订单不存在   | 调整商户订单号      |
| 90006 | INVALID_PROTOCOL_SCENE_CODE       | 无效的 protocolSceneCode | 调整场景代码        |
| 90007 | EXPIREDTIME_ILLEGAL               | 过期时间非法             | 调整过期时间        |
| 90008 | EXPIREDTIME_LESS_THAN_REQUESTTIME | 过期时间小于请求时间     | 调整过期时间        |
| 90009 | INVALID_ACCESS_TYPE               | 无效的 accessType        | 调整请求参数        |

## 业务状态字段速查

返回码为 `0`
