---
title: PayBy收单API总览
domain: payby-acquire-api
kind: wiki_page
slug: payby-acquire-api-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p13
tags: []
---

# PayBy收单API总览

本页汇总 PayBy 收单/退款/单笔付款到账户相关 HTTP API 的目录、公共请求/响应约定与通用返回码，便于在各接口详情页之间导航。

## 接口目录

- [[api_payby_refund_get_order]]：查询退款订单，依据 refundMerchantOrderNo 或 PayBy orderNo 二选一查询退款状态。
- [[api_payby_transfer_place_order]]：单笔付款到账户下单，向用户账户付款（个人手机号/企业 MEMBER_ID）。
- [[api_payby_transfer_get_order]]：查询单笔付款到账户订单，按 merchantOrderNo 返回付款详细结果。
- 业务说明参见 [[payby-transfer-to-account]]。

## 接口域名约定

| 环境 | Base URL |
| --- | --- |
| 联调（UAT） | https://uat.test2pay.com |
| 生产 | https://api.payby.com |

各接口路径：

- 查询退款订单：`/sgs/api/acquire2/refund/getOrder`
- 单笔付款到账户下单：`/sgs/api/transfer/placeTransferOrder`
- 查询单笔付款到账户订单：`/sgs/api/transfer/getTransferOrder`

## 公共 HTTP Header

请求 Header：

| 字段 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | 例 `en` |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

响应 Header：

| 字段 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | sign | Required | String |

## 公共 HTTP Body 结构

请求 Body：

- `requestTime`：Timestamp(3)，必填，毫秒时间戳。
- `bizContent`：各接口对应的业务请求对象（如 `GetRefundOrderRequest` / `PlaceTransferOrderRequest` / `GetTransferOrderRequest`）。

响应 Body：

- `head`：`ResponseHeader`，必填，包含 `applyStatus`、`code`、`msg`，部分场景含 `traceCode`。
- `body`：可选，仅在 `applyStatus=SUCCESS` 且 `code=0` 时返回，结构按接口区分。

## 通用返回码

下列返回码在收单/退款/转账类接口中通用：

| code | msg | 含义 |
| --- | --- | --- |
| 0 | SUCCESS | 成功 |
| 400 | INVALID_PARAMETER | 参数错误 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间过早 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间过晚 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 |
| 403 | UNAUTHORIZED | API 未授权 |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 |
| 500 | SYSTEM_ERROR | 系统错误 |
| 504 | SERVICE_TIMEOUT | 服务超时 |
| 601 | RISK_FAIL | 风控校验失败 |

各接口业务返回码（如 `MERCHANT_ORDER_NO_EXIST`、`ORDER_SUCCESS`、`BENEFICIARY_NOT_EXIST`、`REFUND_MERCHANT_ORDER_NO_NOT_EXIST` 等）见对应接口详情页。

## 通用业务约定

- 订单查询类接口的请求体通常以 `merchantOrderNo` 或 `orderNo`/`refundMerchantOrderNo` 作为唯一定位键。
- 涉及收款人姓名、收款人标识等敏感字段需加密传输（如 `beneficiaryFullName`、`beneficiaryIdentity`）。
- 金额字段统一使用 `Money`（含 `amount`、`currency`，示例币种 `AED`）。
- 订单状态机以业务侧定义为准，单笔付款到账户使用 `CREATED` / `SUCCESS` / `FAILURE`。
