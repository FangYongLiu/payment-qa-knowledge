---
title: PayBy 转账到银行账户返回码总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-return-codes
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p3
tags: []
---

# PayBy 转账到银行账户返回码总览

本页汇总 PayBy 转账到银行账户业务域内涉及的全部返回码（`code` / `msg`），并给出常见原因和处理建议，便于联调与生产排障对照查阅。接口使用上下文请参见 [[payby-transfer-to-bank-overview]]。

## 使用说明

- 返回码统一通过响应 `head.code` 与 `head.msg` 返回；`code = 0` 且 `msg = SUCCESS` 表示业务成功。
- 通知场景下，商户收到 [[api_payby_transfer_to_bank_notify]] 后应返回字符串 `SUCCESS` 表示成功接收，其他视为异常并触发 PayBy 重试。
- 若状态不明或长时间未收到通知，应主动调用 [[api_payby_get_transfer_to_bank_order]] 查询确认订单最终状态。

## 通用返回码

适用于所有转账到银行账户接口（创建、查询等）的公共错误码。

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API 未授权 | 联系 PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 | 联系 PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系 PayBy，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |

## 订单状态相关返回码

涉及订单生命周期与商户订单号校验的错误码。

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 62002 | ORDER_FAILURE | 已失败的订单再次发起撤销；已失败的订单发起退款 | 调整商户订单号 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同，但业务参数不同的创建订单请求 | 调整订单号 |
| 62028 | ORDER_SUCCESS | 订单已成功 | 调整商户订单号 |
| 62029 | ORDER_CREATED | 订单已创建 | 调整商户订单号 |

## 产品与渠道能力相关返回码

涉及产品开通、出款渠道支持范围的错误码。

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 | 请申请产品 |
| 62076 | FUND_OUT_ABILITY_SUPPORTED | `networkCode` 或 `fundoutCurrencyCode` 未开通或不支持 | 联系 PayBy |

## 收款方信息校验返回码

涉及 IBAN、姓名、地区编码等收款方信息字段的校验错误。

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 62101 | WRONG_IBAN_FORMAT | 传入的 IBAN 格式不对 | 调整 `iban` |
| 62102 | NAME_NOT_FOUND | 无法通过 IBAN 查询姓名 | 调整 `iban` |
| 62103 | QUERY_API_UNAVAILABLE | 查询接口不可用 | 稍后重试 |
| 62094 | THE_ENTERED_COUNTRY_CODE_IS_INVALID | 国家码校验失败 | 调整请求参数 |
| 62095 | THE_ENTERED_CITY_CODE_IS_INVALID | 城市码校验失败 | 调整请求参数 |

## 排查建议

- `400` 类参数错误：优先核对请求体字段格式与 `requestTime`（毫秒级时间戳，且不能与服务端时间偏差过大）。
- `403 / 404 / 62026 / 62076`：属于授权或产品/渠道未开通范畴，需联系 PayBy 配置后才能恢复。
- `500 / 504`：系统侧异常或超时，建议结合 [[api_payby_get_transfer_to_bank_order]] 查询订单真实状态后再决定是否重试，避免重复转账。
- `62016 / 62028 / 62029`：均代表 `merchantOrderNo` 已被占用，新建请求需更换商户订单号。
- `601 RISK_FAIL`：触发风控规则，需要业务侧调整请求内容或联系 PayBy 排查。
