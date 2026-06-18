---
title: PayBy收单API总览
domain: payby-acquire-api
kind: wiki_page
slug: payby-acquire-api-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p16
tags: []
---

# PayBy收单API总览

本页汇总 PayBy 收单与会员相关 API 的索引及公共说明，便于快速定位接口与对接规范。

## 接口索引

| 接口 | 用途 | 详情 |
| --- | --- | --- |
| 更新订单超时时间 | 调整订单过期时间（仅限调用时间起 15 天内） | [[api_payby_update_expired_time]] |
| 查询会员余额 | 查询会员账户可用余额 | [[api_payby_get_member_balance]] |

## 环境与地址约定

- 联调域名：`https://uat.test2pay.com`
- 生产域名：`https://api.payby.com`
- 各接口路径见对应子页面。

## 公共请求规范

Http Header（所有接口通用）：

| 字段名 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | 例如 `en`-英文 |
| 签名 | Sign | Required | String | 请求签名 |
| 商户号 | Partner-Id | Required | String(12) | 商户ID |

Http Body 公共字段：

- `requestTime`：Required，Timestamp(3)，毫秒时间戳。
- `bizContent`：Required，业务内容对象，结构因接口而异。

## 公共响应规范

- Http Header 必带 `sign` 签名字段。
- Http Body 包含 `head`（ResponseHeader）和可选 `body`。
- `body` 仅在 `head.applyStatus = SUCCESS` 且 `head.code = 0` 时返回。
- `head` 字段示例：`applyStatus`、`code`、`msg`、`success`、`traceCode`。

## 通用返回码

下列返回码在收单/会员类接口中普遍适用，接口特有错误码参见对应子页：

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

接口特定返回码：

- `62089 INVALID_EXPIRED_TIME`：见 [[api_payby_update_expired_time]]
- `78001 CURRENCY_CODE_NOT_SUPPORTED`：见 [[api_payby_get_member_balance]]
