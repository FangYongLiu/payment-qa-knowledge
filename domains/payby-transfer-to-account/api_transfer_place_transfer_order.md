---
id: api_transfer_place_transfer_order
object_type: API
domain: payby-transfer-to-account
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-v1.1-p1
tags:
- transfer
- 企业付款
- 下单
subdomain: null
module: null
sensitivity: normal
name: 单笔付款到账户接口 (placeTransferOrder)
aliases:
- placeTransferOrder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
企业付款到用户PayBy账户的下单接口，为企业提供付款到用户账户的能力。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/transfer/placeTransferOrder
- 生产URL: https://api.payby.com/sgs/api/transfer/placeTransferOrder
- 提交方式: POST，HTTPS，JSON，UTF-8
- 签名算法: SHA256WithRSA
- 状态机:
  - CREATED: 已创建
  - SUCCESS: 已成功
  - FAILURE: 已失败

## 入参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en | en-英文 |
| 签名 | Sign | Required | String | | |
| 商户号 | Partner-Id | Required | String(12) | | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 | |
| 业务内容 | bizContent | Required | PlaceTransferOrderRequest | - | 业务内容 |

### PlaceTransferOrderRequest
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | Me23484 | |
| 用户标识类型 | beneficiaryIdentityType | Required | String(20) | PHONE_NO | PHONE_NO / MEMBER_ID / TOTOK_UID |
| 用户标识 | beneficiaryIdentity | Required | String(20) | +971-585812345 | 个人用手机号(带区号)，企业用MEMBER_ID。加密传输 |
| 收款用户姓名 | beneficiaryFullName | Optional | String(100) | 李小龙 | 上传姓名则强制校验姓名。加密传送 |
| 金额 | amount | Required | Money | 12.34 | 企业付款金额 |
| 企业付款备注 | memo | Required | String(128) | 奖金 | 付款备注 |
| 后端通知地址 | notifyUrl | Optional | String(200) | - | 商户接收通知的地址 |

### 请求样例
```json
Http Header
{
    "Content-Language": "en",
    "Content-Type": "application/json",
    "Partner-Id": "200000018132",
    "sign": "ODOK+d0os7q0FTWNKGTr6Yt3FlO6alfvIp+IhHfudxQZ..."
}

Http Body
{
    "bizContent": {
        "amount": {"amount": 1.21, "currency": "AED"},
        "beneficiaryFullName": "SgsiXi2T//eEymXADGbK7o0EE9wmCTQxi4gLNp7y1JYTW0Pb...",
        "beneficiaryIdentity": "KUsQ3GNU/1p11hVHNljTQehKtjqhIvtED1aOcWuVqY2puGqi...",
        "beneficiaryIdentityType": "PHONE_NO",
        "memo": "Your memo",
        "merchantOrderNo": "M021482754853",
        "notifyUrl": "http://www.yoursite.com"
    },
    "requestTime": 1585142886252
}
```

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 签名 | sign | Required | String | |

### Http Body（body 仅在 applyStatus=SUCCESS 且 code=0 时返回）
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader | |
| 响应体 | body | Optional | PlaceTransferOrderResponse | |

### PlaceTransferOrderResponse
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 订单信息 | transferOrder | Required | TransferOrder | 付款到账户订单信息 |

### 响应样例
```json
Http Header
{
    "sign": "WzVWAdy4Z+tMhgqtuxle+R9P3R3Yn5uMeICj8jIFTBpfReJLviZY..."
}

Http Body
{
    "head": {
        "applyStatus": "SUCCESS",
        "code": "0",
        "msg": "SUCCESS",
        "traceCode": "1127"
    },
    "body": {
        "transferOrder": {
            "amount": {"amount": 1.21, "currency": "AED"},
            "beneficiaryFullName": "5a0d9e4fd01a40ff3ab89dfde84c2253b5ea07c4ba8b4e5f25b81df3b73b9db0",
            "beneficiaryIdentity": "a25c5bff2fabf6bccf8ff13a940f5d05d3927c1501373ac6fa129d4fa688417c",
            "beneficiaryIdentityType": "PHONE_NO",
            "memo": "company single pay",
            "merchantOrderNo": "M021482754853",
            "notifyUrl": "http://qa.test2pay.com/api/notification",
            "orderNo": "911585142879004849",
            "paymentInfo": {
                "arrivalTime": 1585142880000,
                "payerFeeAmount": {"amount": 0, "currency": "AED"}
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
| 500 | SYSTEM
