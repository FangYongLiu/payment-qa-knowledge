---
id: api_payby_get_transfer_to_bank_card
object_type: API
domain: fund-out-transfer
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-bankcard-v0.2-p3
tags:
- transfer
- bank-card
- query
subdomain: null
module: null
sensitivity: normal
name: 查询转账银行卡接口
aliases:
- getTransferToBankCard
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures:
- payby-transfer-to-bank-return-codes
---

## 用途
用于查询转账到银行卡的结果，返回付款的详细结果。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/transfer/getTransferToBankCard
- 生产URL: https://api.payby.com/sgs/api/transfer/getTransferToBankCard
- 方法: HTTP POST (application/json)

## 入参

### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 示例 1581493898000 |
| 业务内容 | bizContent | Required | GetTransferToBankOrderRequest | 业务内容 |

### GetTransferBankCardRequest
| 字段名 | 变量名 | 必填 | 类型 | 示例值 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | Me23484 |

## 出参

### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | PlaceTransferToBankOrderResponse |

### PlaceTransferToBankOrderResponse
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 订单信息 | transferBankCardOrder | Required | TransferBankCardOrder |

响应样例中 body 实际包裹字段为 `transferToBankCard`，包含字段：amount(amount/currency)、partnerId、notifyUrl、memo、createdTime、payerFeeAmount、payerFeeMemberId、orderNo、merchantOrderNo、product、status(如 CREATED)、paidTime、accountHolderType(如 INDIVIDUAL)、cardNumber、expiryMonth、expiryYear、firstName、lastName、middleName。

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
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy,稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |

## 测试校验点
- Header 必填项校验：Sign、Partner-Id 缺失或错误时返回 INVALID_PARAMETER 或 UNAUTHORIZED。
- requestTime 偏移校验：过早返回 REQUESTTIME_TOO_EARLY，过晚返回 REQUESTTIME_TOO_LATER。
- bizContent.merchantOrderNo 必填，长度 ≤ 64。
- 不存在的 merchantOrderNo 返回 62004 MERCHANT_ORDER_NO_NOT_EXIST。
- 高频请求触发 402 RATE_LIMIT_REJECT。
- 未授权或未申请产品访问返回 403 UNAUTHORIZED / 404 SERVICE_NOT_AVAILABLE。
- 成功响应 head.code=0、msg=SUCCESS，且 transferToBankCard 中 orderNo、merchantOrderNo、status、amount(amount/currency)、cardNumber、expiryMonth、expiryYear、firstName/lastName 等字段齐全。
- status 取值校验（如 CREATED 等）与 paidTime/createdTime 时间合理性。
- 敏感字段（cardNumber、firstName、lastName、middleName）应为加密/脱敏值。
- payerFeeAmount 与 payerFeeMemberId 一致性校验。
- 签名响应验签：使用 PayBy 公钥校验响应 Sign。
