---
title: PayBy收单API总览
domain: payby-acquire-api
kind: wiki_page
slug: payby-acquire-api-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p11
tags: []
---

# PayBy收单API总览

本页汇总 PayBy 收单 API 系列接口的整体说明与公共约定，覆盖接口清单、统一的请求/响应结构、签名与商户号要求，以及通用错误码。各接口的具体字段与样例见对应子页。

## 接口清单

当前已纳入 PayBy 收单 API 系列的接口：

- [[api_payby_acquire_cancel_order]]：取消订单（`/sgs/api/acquire2/cancelOrder`），用于支付失败重发前撤销原单、或用户支付超时后系统主动取消订单。
- [[api_payby_acquire_get_order]]：查询订单（`/sgs/api/acquire2/getOrder`），用于主动查询订单状态、确认支付/冲正结果，作为通知缺失或未知交易状态的兜底手段。

## 环境与接口地址

所有收单接口均提供两套环境，路径前缀统一为 `/sgs/api/acquire2/`：

- 联调（UAT）：`https://uat.test2pay.com`
- 生产：`https://api.payby.com`

## 公共请求结构

### Http Header

| 字段名 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 文案语言 | `Content-Language` | Optional | String(10) | 如 `en` 表示英文 |
| 签名 | `sign` | Required | String | 请求签名 |
| 商户号 | `Partner-Id` | Required | String(12) | PayBy 分配的商户号 |

> 注：查询订单接口 Header 中签名字段名在文档中以 `Sign` 给出，取消订单为 `sign`，实际以各接口页为准。

### Http Body

| 字段名 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 请求时间 | `requestTime` | Required | Timestamp(3) | 毫秒级时间戳 |
| 业务内容 | `bizContent` | Required | OrderIndexRequest | 各接口业务参数 |

收单系列接口的 `bizContent` 复用 `OrderIndexRequest`，最常用字段为 `merchantOrderNo`（商户订单号）。

## 公共响应结构

### Http Header

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | `sign` | Required | String |

### Http Body

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | `head` | Required | ResponseHeader |
| 响应体 | `body` | Optional | 各接口响应对象（如 `CancelOrderResponse`、`GetOrderResponse`） |

约定：**仅当 `head.applyStatus = SUCCESS` 且 `head.code = 0` 时，才会返回 `body` 字段**。

`body` 中的核心对象为 `acquireOrder`（AcquireOrder），常见字段包括：

- 订单标识：`merchantOrderNo`、`orderNo`
- 状态：`status`（如 `SETTLED`、`FAILURE` 等）、`revoked`（冲正状态，`true` 表示冲正成功）
- 金额：`totalAmount`、`paymentInfo.paidAmount`、`payeeFeeAmount`、`payerFeeAmount`
- 交易信息：`paymentInfo`（含 `paidTime`、`payerMid`、`payChannel` 等）、`payeeMid`、`paySceneCode`
- 业务附加：`product`、`subject`、`reserved`、`notifyUrl`、`expiredTime`、`requestTime`
- 附属内容：`accessoryContent`（含 `amountDetail`、`goodsDetail`、`terminalDetail`）

## 通用返回码

以下返回码为收单系列接口共用：

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
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |
| 62035 | ORDER_NO_NOT_EXIST | PayBy订单号的订单不存在 | 调整PayBy订单号 |

接口私有的返回码（如 `cancelOrder` 的 `62001 ORDER_PAID`、`62002 ORDER_FAILURE`、`62003 ORDER_SETTLED`）见各接口页。

## 使用建议

- 调用关单 / 撤销前，先用查询订单确认当前支付状态，避免误操作。
- 商户系统未收到支付通知、或下单返回未知状态时，应主动调用查询订单兜底。
- 判断冲正是否成功：以 `acquireOrder.revoked = true` 为准。

详见：[[api_payby_acquire_cancel_order]]、[[api_payby_acquire_get_order]]。
