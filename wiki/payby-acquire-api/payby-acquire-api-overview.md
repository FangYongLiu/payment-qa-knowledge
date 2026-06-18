---
title: PayBy收单API总览
domain: payby-acquire-api
kind: wiki_page
slug: payby-acquire-api-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p9
tags: []
---

# PayBy收单API总览

本页概述 PayBy 收单接口家族的整体定位、订单状态机及通用约定，作为各具体接口（如创建订单等）的入口与索引。

## 接口家族定位

- 商户系统先调用 PayBy 收单接口在 PayBy 服务后台生成预支付订单。
- 接口返回订单会话标识（Token）后，由商户调起后续支付。
- 收单接口家族围绕 `AcquireOrder` 这一核心订单实体进行 创建 / 支付 / 结算 / 预授权 / 取消 等生命周期操作。

## 订单状态机（AcquireOrderStatus）

| Status | 说明 |
| --- | --- |
| CREATED | 已创建 |
| PAID_SUCCESS | 支付成功 |
| SETTLED | 结算成功 |
| FAILURE | 订单失败 |
| AUTHORIZATION | 预授权成功 |
| VOID | 预授权取消成功 |

说明：

- `CREATED` 是订单初始态；仅在订单状态为 `CREATED` 时，创建订单接口会根据不同 `paySceneCode` 返回对应的 `interactionParams`。
- 已 `PAID_SUCCESS` / `SETTLED` / `FAILURE` 的订单再次发起创建会返回相应错误码（见下文通用返回码）。

## 接口家族成员

- [[api_acquire_place_order]]：创建订单接口（placeOrder），用于在 PayBy 后台生成预支付订单并返回支付参数。

## 通用约定

### 接入环境

- 联调（UAT）域名：`https://uat.test2pay.com`
- 生产域名：`https://api.payby.com`
- 收单接口路径前缀：`/sgs/api/acquire2/`

### 通用 Http Header

| 字段名 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文（默认） |
| 签名 | sign | Required | String | 请求/响应均带签名 |
| 商户号 | Partner-Id | Required | String(12) | 仅请求侧 |

### 通用 Http Body 结构

- 请求：`requestTime`（Timestamp(3)） + `bizContent`（具体业务请求对象）。
- 响应：`head`（ResponseHeader） + `body`（具体业务响应对象，仅在 `applyStatus=SUCCESS` 且 `code=0` 时返回）。

### 幂等性

- 收单接口为幂等接口：相同请求重复调用会返回当前订单状态。
- 幂等请求不校验请求时间；多次请求时，订单的请求时间以**第一次**请求的 `requestTime` 为准。

## 通用返回码

下列返回码在收单接口家族中通用：

| code | msg | 原因 |
| --- | --- | --- |
| 0 | SUCCESS | 成功 |
| 400 | INVALID_PARAMETER | 参数错误 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 |
| 403 | UNAUTHORIZED | API 未授权 |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 |
| 500 | SYSTEM_ERROR | 系统错误 |
| 504 | SERVICE_TIMEOUT | 服务超时 |
| 601 | RISK_FAIL | 风控校验失败 |

业务相关返回码（如 `ORDER_PAID`、`ORDER_FAILURE`、`ORDER_SETTLED`、`EXPIREDTIME_*`、`PAYSCENECODE_ILLEGAL`、`MERCHANT_ORDER_NO_EXIST`、`PAYERMID/PAYEEMID_*` 等）在具体接口页详述，参见 [[api_acquire_place_order]]。
