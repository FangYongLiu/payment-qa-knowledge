---
title: PayBy转账到银行账户返回码总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-return-codes
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-bankcard-v0.2-p3
tags: []
---

# PayBy转账到银行账户返回码总览

本页汇总 PayBy 转账到银行账户业务域下所有接口可能返回的 `code`/`msg`，包含原因说明与建议解决方案，便于排障与对接联调。相关接口见 [[payby-transfer-to-bank-overview]]、[[api_payby_get_transfer_to_bank_card]]、[[api_payby_transfer_bank_card_notify]]。

## 通用返回码

适用于所有转账到银行卡相关接口的通用错误。

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |

## 业务返回码

针对订单状态/订单号等业务校验失败的错误码。

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 62002 | ORDER_FAILURE | 已失败的订单再次发起撤销；已失败的订单发起退款 | 调整商户订单号 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同，不同业务参数的创建订单请求 | 调整订单号 |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 | 请申请产品 |
| 62028 | ORDER_SUCCESS | 订单已成功 | 调整商户订单号 |
| 62029 | ORDER_CREATED | 订单已创建 | 调整商户订单号 |

## 接口适用范围说明

- [[api_payby_get_transfer_to_bank_card]]（查询转账银行卡）：常见返回码为 `0`、`400`、`402`、`403`、`404`、`500`、`504`、`601`、`62004`。
- 其余 `62002`、`62016`、`62026`、`62028`、`62029` 为转账到银行账户业务域下创建/撤销/退款等订单类操作可能产生的码。
- 通知场景见 [[api_payby_transfer_bank_card_notify]]，商户收到通知后应返回 `SUCCESS` 表示成功接收，其他视为异常并触发重试。

## 排障建议

- `400` 系列：先核对请求参数与 `requestTime` 时间戳（毫秒）是否在合理窗口内。
- `402` / `504`：客户端做退避重试，避免高频冲击。
- `403` / `404` / `62026`：权限或产品未开通，联系 PayBy 申请开通。
- `500`：先稍后重试，仍失败联系 PayBy 并提供 `traceCode`。
- `601`：触发风控，复核业务合规性后再发起。
- `62004` / `62016` / `62028` / `62029`：通过调整 `merchantOrderNo` 或确认订单当前状态后再继续操作。
- `62002`：订单已为失败态，不应再发起撤销/退款。
