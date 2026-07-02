---
id: api_transfer_get_transfer_order
object_type: API
domain: wallet
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-v1.1-p1
tags:
- query
- transfer
subdomain: null
module: null
sensitivity: normal
name: 查询单笔付款到账户订单接口 (getTransferOrder)
aliases:
- getTransferOrder
related_services:
- svc_transfer
---

## 用途
用于单笔付款到账户的结果查询，根据商户订单号(merchantOrderNo)返回付款到账户订单的详细结果。

## 路径/方法
- 联调URL: `https://uat.test2pay.com/sgs/api/transfer/getTransferOrder`
- 生产URL: `https://api.payby.com/sgs/api/transfer/getTransferOrder`
- 提交方式: POST
- 传输方式: HTTPS
- 数据格式: JSON
- 字符编码: UTF-8
- 签名算法: SHA256WithRSA（请求和响应都需签名）

## 入参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 示例值 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 |
| 业务内容 | bizContent | Required | GetTransferOrderRequest | - |

### GetTransferOrderRequest
| 字段名 | 变量名 | 必填 | 类型 | 示例值 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | Me23484 |

### 请求样例
```json
Http Header
{
    "Content-Language": "en",
    "Content-Type": "application/json",
    "Partner-Id": "200000018132",
    "sign": "WF34t3rh4wuBuiUqlAte0PErySJBrwWEuNAgP5DYTZnI5fah0xC0desDOcLAakN1E6UccD8Yq4zuNBtkmLdA74eSkk2lb5+k+lP9/a5Aa7h12UtLc62JDpzQL/O3NgvPJCDBCat2Mmso5ihNOWKGyw/L4YhaqSrqHGfVEimiyrY/giBPJ5Ktof6Qyy2AiSNMAJPNzYFu73Kmc3ogYUKh487hLTNHGPPBsqPTIOO10+wG9/q0I3P90uOqXCYkoq7JyU3j1WkRZp5YmKTvIcfe4EJ/tsVtvBPVOw4ParnWD6nMlA59/y8K4D+wwZd7exbA/r85FRBkW+JdsY1z+yQJ7Q=="
}

Http Body
{
    "bizContent": {
        "merchantOrderNo": "M021482754853"
    },
    "requestTime": "1585143324254"
}
```

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | sign | Required | String |

### Http Body
仅当 applyStatus 为 SUCCESS 且 code 为 0 时才返回 body。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | GetTransferOrderResponse |

### GetTransferOrderResponse
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 订单信息 | transferOrder | Required | TransferOrder | 付款到账户订单信息 |

### 响应样例
```json
Http Header
{
    "sign": "I1zfK8Bdfti5+PS0Q1PEdPlS77jF4SaJLRMbgWaisFgUSIW0It03Mk2YCTamWWzVN9ElGd1ditgvWS5/Kjff+yZofnVGc1UQQ2x3sfyz7Z8IL1lLz9KiM4c55b02gILe7VEecJox/Yu6fgURKb0GK3GRxgeUbzoqsIrDlHZ4cy5A1tNf5lAhaVOQ1Zfao0jc+l6nIW7gRhcZb/gOBrEGT5MkNLPbnwUxSkWDISlN3/IOBYgE5Eoaq+lbZO2ji7Xr0AsfKoC9sueVLeubbDRHWgN6fi1vewqA5FFKACS1+UUeXqR/x95MTR0cR6qnfOodf0c09GGyrTIR+x3M0vkFPw=="
}

Http Body
{
    "head": {
        "applyStatus": "SUCCESS",
        "code": "0",
        "msg": "SUCCESS",
        "traceCode": "1125"
    },
    "body": {
        "transferOrder": {
            "amount": {
                "amount": 1.21,
                "currency": "AED"
            },
            "beneficiaryFullName": "5a0d9e4fd01a40ff3ab89dfde84c2253b5ea07c4ba8b4e5f25b81df3b73b9db0",
            "beneficiaryIdentity": "a25c5bff2fabf6bccf8ff13a940f5d05d3927c1501373ac6fa129d4fa688417c",
            "memo": "company single pay",
            "merchantOrderNo": "M021482754853",
            "notifyUrl": "http://www.yoursite.com",
            "orderNo": "911585142879004849",
            "paymentInfo": {
                "arrivalTime": 1585142880000,
                "payerFeeAmount": {
                    "amount": 0,
                    "currency": "AED"
                }
            },
            "product": "Transfer",
            "requestTime": 1585142886252,
            "status": "SUCCESS"
        }
    }
}
```

## 错误码
| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayB
