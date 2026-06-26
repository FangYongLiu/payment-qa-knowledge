---
title: PayBy收单API总览
domain: payby-open-api
kind: wiki_page
slug: payby-acquiring-api-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p12
tags: []
related_services:
  - svc_acquireii
  - svc_sgs
related_tables:
  - tbl_acquireii_t_acquire_order
  - tbl_acquireii_t_refund_order
---

# PayBy收单API总览

本页汇总 PayBy 收单（acquiring）API 的整体信息，作为各接口子页的导航入口与通用约定参考。

## 接口清单

当前业务域包含的接口：

- [[api_payby_refund_place_order]]：退款下单接口（`/sgs/api/acquire2/refund/placeOrder`），用于对原收单订单发起退款。

## 环境与基础地址

各接口共用以下环境域名，子接口在其后追加自身路径：

- 联调（UAT）：`https://uat.test2pay.com`
- 生产：`https://api.payby.com`

## 通用请求约定

所有接口在 HTTP 层遵循相同的头部与请求体结构。

### 通用 Http Header

| 字段名 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | 例：`en` 表示英文 |
| 签名 | Sign | Required | String | 请求签名 |
| 商户号 | Partner-Id | Required | String(12) | PayBy 分配 |

### 通用 Http Body 外层

| 字段 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 毫秒时间戳 |
| 业务内容 | bizContent | Required | 各接口对应请求对象 | 业务内容载体 |

## 通用响应约定

- 响应 Header 中包含 `sign` 字段，用于签名校验。
- 响应 Body 由 `head`（ResponseHeader）与 `body`（接口具体响应对象）组成。
- `body` 仅当 `head.applyStatus = SUCCESS` 且 `head.code = 0` 时返回。

## 通用返回码

以下返回码为收单 API 共用的基础码，业务相关码请参见各接口子页。

| code | msg | 含义 | 处理建议 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间过早 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间过晚 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API 未授权 | 联系 PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 | 联系 PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 稍后重试或联系 PayBy |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 调整业务 |

## 通用数据类型

接口报文中重复出现的复合类型：

- `Money`：包含 `currency` 与 `amount` 两个字段，用于表示金额（如 `{"currency":"AED","amount":0.01}`）。
- `ResponseHeader`：响应头对象，含 `applyStatus`、`code`、`msg`。

## 导航

- 退款相关：[[api_payby_refund_place_order]]
