---
title: PayBy转账到银行账户总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-bankcard-v0.2-p2
tags: []
---

# PayBy转账到银行账户总览

PayBy转账到银行账户接口用于商户将自有账户资金付款到指定收款银行卡，当前业务域包含单笔转账银行卡能力。

## 应用场景

- 商户将账户中的资金付款到指定的收款银行账户。
- 支持账户持有人类型：`INDIVIDUAL`、`CORPORATE`。
- 支持发送方类型（senderType）：`INDIVIDUAL`、`CORPORATE`；当为 `INDIVIDUAL` 时，必须提供 `senderInfoRequest`。

## 订单状态机

| Status    | 说明     |
| --------- | -------- |
| CREATED   | 已创建   |
| SUCCESS   | 已成功   |
| FAILURE   | 已失败   |
| BANK_FAIL | 银行退票 |

## 接口清单

| 接口 | 说明 |
| --- | --- |
| [[api_payby_place_transfer_to_bank_card]] | 单笔转账到银行卡（placeTransferToBankCard） |

## 环境地址

- 联调（UAT）：`https://uat.test2pay.com/sgs/api/transfer/placeTransferToBankCard`
- 生产：`https://api.payby.com/sgs/api/transfer/placeTransferToBankCard`

## 通用约定

- 请求/响应 Http Header 必带：`sign`、`Partner-Id`；可选 `Content-Language`（如 `en`）。
- 敏感字段（如 `firstName`、`lastName`、`middleName`、`companyName`、`cardNumber`、`expiryYear`、`expiryMonth` 等）需加密传输。
- 当传入 `cardToken` 时，卡相关字段（卡号、有效期）以 `cardToken` 查询结果为准；此时 `last4` 必输。
- 跨境转账场景下，发送方 `dateOfBirth` 必填。

## 通用返回码

| code  | msg                     | 原因                                  | 解决方案           |
| ----- | ----------------------- | ------------------------------------- | ------------------ |
| 0     | SUCCESS                 | 成功                                  |                    |
| 400   | INVALID_PARAMETER       | 参数错误                              | 调整请求参数       |
| 400   | REQUESTTIME_TOO_EARLY   | 请求时间比当前时间早太多              | 调整请求时间       |
| 400   | REQUESTTIME_TOO_LATER   | 请求时间比当前时间晚太多              | 调整请求时间       |
| 402   | RATE_LIMIT_REJECT       | 请求过于频繁                          | 降低请求频率       |
| 403   | UNAUTHORIZED            | API未授权                             | 联系PayBy          |
| 404   | SERVICE_NOT_AVAILABLE   | API服务不可用                         | 联系PayBy          |
| 500   | SYSTEM_ERROR            | 系统错误                              | 联系PayBy,稍后重试 |
| 504   | SERVICE_TIMEOUT         | 服务超时                              | 稍后重试           |
| 601   | RISK_FAIL               | 风控校验失败                          | 请调整业务         |
| 62002 | ORDER_FAILURE           | 订单已失败                            | 调整商户订单号     |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同,不同业务参数的创建订单请求 | 调整订单号         |
| 62026 | PRODUCT_IS_NOT_APPLIED  | 产品未申请                            | 请申请产品         |
| 62028 | ORDER_SUCCESS           | 订单已成功                            | 调整商户订单号     |
| 62029 | ORDER_CREATED           | 订单已创建                            | 调整商户订单号     |
