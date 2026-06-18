---
title: PayBy转账到银行接口返回码总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-return-codes
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p2
tags: []
---

# PayBy转账到银行接口返回码总览

本页汇总 PayBy 转账到银行业务域下各接口的返回码、含义及处理建议，便于联调与排障。相关接口说明见 [[payby-transfer-to-bank-overview]]。

## 通用返回码

以下返回码在 [[api_transfer_calculate_fundout]] 与 [[api_transfer_place_to_bank_order]] 两个接口中通用：

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy,稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |

## 出款试算专属返回码

适用于 [[api_transfer_calculate_fundout]]：

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 62076 | FUND_OUT_ABILITY_SUPPORTED | networkCode 或 fundoutCurrencyCode 未开通或不支持 | 联系PayBy |

## 单笔付款到银行卡专属返回码

适用于 [[api_transfer_place_to_bank_order]]：

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 62002 | ORDER_FAILURE | 订单已失败 | 调整商户订单号 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同,不同业务参数的创建订单请求 | 调整订单号 |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 | 请申请产品 |
| 62028 | ORDER_SUCCESS | 订单已成功 | 调整商户订单号 |
| 62029 | ORDER_CREATED | 订单已创建 | 调整商户订单号 |
| 62094 | THE_ENTERED_COUNTRY_CODE_IS_INVALID | 国家码校验失败 | 调整请求参数 |
| 62095 | THE_ENTERED_CITY_CODE_IS_INVALID | 城市码校验失败 | 调整请求参数 |

## 排查建议

- `400` 类错误：优先检查参数完整性、字段长度、`requestTime` 与服务器时差。
- `402/504`：客户端做退避重试，避免高频冲击。
- `403/404/500`：基本属于服务侧或授权问题，需联系 PayBy。
- `601`：触发风控，复核业务合规性后再发起。
- `62016 / 62028 / 62029`：均与 `merchantOrderNo` 唯一性相关，重复下单或参数不一致时应使用新的商户订单号。
- `62094 / 62095`：核对 `countryCode`、`cityCode` 取值是否符合 PayBy 支持范围。
- `62076`：试算前确认 `networkCode`（SWIFT / LOCAL）与 `fundoutCurrencyCode` 已对该商户开通。
