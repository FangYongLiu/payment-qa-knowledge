---
id: api_payby_place_transfer_to_bank_card
object_type: API
domain: fund-out-transfer
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-bankcard-v0.2-p2
tags:
- transfer
- bank-card
- payout
subdomain: null
module: null
sensitivity: normal
name: 单笔转账到银行卡接口(placeTransferToBankCard)
aliases:
- placeTransferToBankCard
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
商户将账户中的资金付款到指定的收款银行卡账户(单笔转账到银行卡)。

订单状态机：
- CREATED 已创建
- SUCCESS 已成功
- FAILURE 已失败
- BANK_FAIL 银行退票

## 路径/方法
- 联调URL: `https://uat.test2pay.com/sgs/api/transfer/placeTransferToBankCard`
- 生产URL: `https://api.payby.com/sgs/api/transfer/placeTransferToBankCard`
- 方法: HTTP POST (JSON)

## 入参

### Http Header
| 字段 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| Content-Language | Optional | String(10) | 文案语言，例如 en |
| sign | Required | String | 签名 |
| Partner-Id | Required | String(12) | 商户号 |

### Http Body
| 字段 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| requestTime | Required | Timestamp(3) | 请求时间，毫秒时间戳 |
| bizContent | Required | PlaceTransferBankCardRequest | 业务内容 |

### PlaceTransferBankCardRequest
| 字段 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| accountHolderType | Required | String(16) | INDIVIDUAL / CORPORATE |
| merchantOrderNo | Required | String(64) | 商户订单号 |
| firstName | Optional | String(35) | 加密传输；INDIVIDUAL 必输；英文字母；2-35 |
| lastName | Optional | String(35) | 加密传输；INDIVIDUAL 必输；英文字母；2-35 |
| middleName | Optional | String(35) | 加密传输；英文字母；2-35 |
| companyName | Optional | String(50) | 加密传输；CORPORATE 必输；不允许单字符/全数字/全标点 |
| amount | Required | Money | 企业付款金额 |
| memo | Optional | String(50) | 付款备注 |
| notifyUrl | Optional | String(200) | 商户接收通知地址 |
| expiryYear | Optional | String(4) | 加密传输；>= 当前年；cardToken 非空时以 cardToken 查询为准 |
| expiryMonth | Optional | String(2) | 加密传输；1-12；year+month >= 当前月；cardToken 非空时以 cardToken 查询为准 |
| cardNumber | Optional | String(50) | 加密传输；长度 12-19；全数字；cardToken 非空时以 cardToken 查询为准 |
| cardToken | Optional | String(32) | 卡 token |
| cardTokenMerchantId | Optional | String(32) |  |
| last4 | Optional | String(4) | cardToken 非空时必输 |
| countryCode | Required | String(2) | 两位 ISO 国家代码 |
| state | Optional | String(3) | AU/CA/US 必输；2-3 个英文字符 |
| zipCode | Optional | String(10) | SA 必输 |
| city | Required | String(50) |  |
| addressLine | Required | String(200) |  |
| senderInfoRequest | Optional | SenderInfoRequest | INDIVIDUAL 时必输 |
| senderType | Required | String(16) | INDIVIDUAL / CORPORATE |

### SenderInfoRequest
| 字段 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| firstName | Required | String(35) | 加密传输；英文字母；2-35 |
| lastName | Required | String(35) | 加密传输；英文字母；2-35 |
| countryCode | Required | String(2) | 两位 ISO 国家代码 |
| state | Optional | String(3) | US 必输；2-3 个英文字符 |
| zipCode | Optional | String(10) | US 必输 |
| city | Required | String(50) |  |
| addressLine | Required | String(200) |  |
| reference | Required | String(15) | sender 唯一标识；仅字母数字；5-15 |
| sourceOfFunds | Required | String(15) | credit / debit / prepaid / deposit_account / mobile_money_account / cash |
| dateOfBirth | Optional | String(10) | YYYY-MM-DD；跨境转账必填 |

## 出参

### Http Header
| 字段 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| Content-Language | Optional | String(10) | en |
| Sign | Required | String | 签名 |
| Partner-Id | Required | String(12) | 商户号 |

### Http Body
| 字段 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| head | Required | ResponseHeader | 响应头(含 applyStatus、code、msg、traceCode) |
| body | Optional | PlaceTransferBankCardResponse | 响应体 |

### PlaceTransferToBankOrderResponse
| 字段 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- |
| transferBankCardOrder | Required | TransferBankCardOrder | 订单信息 |

响应样例中 body 实际包含 `transferToBankCard` 对象，关键字段：
- amount(Money)
- partnerId、notifyUrl、memo、requestTime
- transferFee(Money)
- orderNo、merchantOrderNo、product、status(CREATED/SUCCESS/FAILURE/BANK_FAIL)、paidTime
- accountHolderType
- cardNumber、expiryMonth、expiryYear(密文返回)
- firstName、lastName、middleName(密文返回)
- countryCode、state、city、addressLine
- senderInfo: firstName、lastName、countryCode、state、zipCode、city、addressLine、reference、sourceOfFunds

## 错误码
| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 |  |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间过早 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间过晚 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API 未授权 | 联系 PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 | 联系 PayBy |
| 500 | SYSTEM_ERROR | 系
