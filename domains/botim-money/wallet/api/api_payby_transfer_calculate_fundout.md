---
id: api_payby_transfer_calculate_fundout
object_type: API
domain: wallet
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: wiki_attachment
source_ref: wiki_attachment:56e8e18c-82c1-4231-b586-2130e089c7da
tags:
- 试算
- 汇率
- 手续费
subdomain: null
module: null
sensitivity: normal
name: 出款试算接口
aliases:
- calculateFundout
related_services:
- svc_transfer
---

## 用途
商户在发起转账到银行账户前，调用该接口试算汇率并返回出款手续费、到账金额等信息。since v2.1。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/transfer/calculateFundout
- 生产URL: https://api.payby.com/sgs/api/transfer/calculateFundout
- 提交方式: HTTPS POST
- 数据格式: JSON, UTF-8
- 签名算法: SHA256WithRSA

## 入参
Http Header

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

Http Body

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 | |
| 网络代码 | networkCode | Required | String(20) | SWIFT | SWIFT / LOCAL |
| 到账币种 | fundoutCurrencyCode | Required | String(20) | USD | |
| 订单金额 | orderAmount | Required | Money | | |

请求样例：
```json
{
    "requestTime":1585142880000,
    "bizContent":{
        "fundoutCurrencyCode":"USD",
        "networkCode":"LOCAL",
        "orderAmount":{
            "amount":100,
            "currency":"AED"
        }
    }
}
```

## 出参
Http Header：Content-Language、Sign、Partner-Id

Http Body

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | CalculateFundoutResult |

CalculateFundoutResult

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 出款信息 | fundoutInfo | Required | FundoutInfo |

FundoutInfo

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 手续费 | feeAmount | Required | Money | | 出款产生的出款手续费，外扣费，不包含在订单金额中 |
| 到账金额 | fundoutAmount | Required | Money | | |
| 订单金额 | orderAmount | Required | Money | | |
| 网络代码 | networkCode | Required | String(20) | SWIFT | SWIFT / LOCAL |
| 汇率 | rate | Required | BigDecimal | 1.33 | rate = fundoutAmount/orderAmount，保留2位小数 |

响应体片段示例：
```json
{
    "fundoutInfo":{
        "fundoutAmount":{"amount":27.21,"currency":"USD"},
        ...
    }
}
```

## 错误码
原文未在本接口章节单独列出返回码（响应被截断）。通用返回码可参考 `payby-transfer-to-bank-return-codes`，常见包括：
- 0 SUCCESS
- 400 INVALID_PARAMETER / REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER
- 402 RATE_LIMIT_REJECT
- 403 UNAUTHORIZED
- 404 SERVICE_NOT_AVAILABLE
- 500 SYSTEM_ERROR
- 504 SERVICE_TIMEOUT
- 601 RISK_FAIL

## 测试校验点
- networkCode 仅支持 SWIFT / LOCAL，错误值应返回 INVALID_PARAMETER。
- fundoutCurrencyCode 必须与所选 networkCode + 商户出款能力匹配（参考 [[api_payby_transfer_get_fundout_ability_list]]）。
- orderAmount 的 amount 与 currency 必填，currency 应为商户支持币种（如 AED）。
- 校验返回 rate = fundoutAmount/orderAmount，且保留2位小数。
- feeAmount 为外扣费，不应包含在 orderAmount 中；校验 fundoutAmount 与 orderAmount、rate 的换算一致性。
- 校验签名（SHA256WithRSA，对原始 Http Body 签名，Base64 编码）；响应也需验签。
- requestTime 偏离当前时间过大应返回 REQUESTTIME_TOO_EARLY / TOO_LATER。
- 高频调用应触发 RATE_LIMIT_REJECT。
- 未授权商户访问应返回 UNAUTHORIZED。
