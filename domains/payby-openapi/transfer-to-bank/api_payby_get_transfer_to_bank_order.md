---
id: api_payby_get_transfer_to_bank_order
object_type: API
domain: payby-openapi
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p14
tags:
- bank
- payout
- query
- transfer
subdomain: transfer-to-bank
module: null
sensitivity: normal
name: 查询单笔付款到银行卡订单
aliases:
- getTransferToBankOrder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures:
- payby-transfer-to-bank-return-codes
---

## 用途
用于单笔付款到银行卡的结果查询，返回付款的详细结果。商户通过商户订单号(merchantOrderNo)查询此前创建的付款到银行卡订单的处理状态及详情。当订单状态不明或未收到 PayBy 异步通知时，建议商户主动调用本接口确认订单状态。

## 路径/方法
- 联调 URL: https://uat.test2pay.com/sgs/api/transfer/getTransferToBankOrder
- 生产 URL: https://api.payby.com/sgs/api/transfer/getTransferToBankOrder
- 协议/方法: HTTP POST，Content-Type: application/json

## 入参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | 商户私钥签名 |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 例: 1581493898000 |
| 业务内容 | bizContent | Required | GetTransferToBankOrderRequest | 业务内容 |

### GetTransferToBankOrderRequest
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
| 响应体 | body | Optional | GetTransferToBankOrderResponse |

ResponseHeader 包含: applyStatus、code、msg、traceCode。

### GetTransferToBankOrderResponse
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 订单信息 | transferToBankOrder | Required | TransferToBankOrder |

### TransferToBankOrder（响应样例字段）
- amount: {amount, currency}（currency 例 AED）
- holderName（加密/脱敏）
- iban（加密/脱敏）
- beneficiaryAddress（加密/脱敏）
- memo
- merchantOrderNo
- notifyUrl
- orderNo
- paymentInfo: {arrivalTime, payerFeeAmount{amount, currency}}
- product，例 "Transfer To Bank"
- requestTime
- status，例 SUCCESS
- swiftCode（响应样例中可能含空格，如 "BBME AEAD"）
- bankReference

### 订单状态机 (status)
| Status | 说明 |
| --- | --- |
| CREATED | 已创建 |
| SUCCESS | 已成功 |
| FAILURE | 已失败 |
| BANK_FAIL | 银行退票 |

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
- Header 必填校验：缺失 Sign / Partner-Id 应拒绝；Content-Language 可选(en)。
- 签名校验：使用商户私钥签名，PayBy 公钥验签；篡改 body 应导致验签失败；响应 Sign 验签通过。
- Body 必填校验：requestTime、bizContent.merchantOrderNo 缺失返回 400 INVALID_PARAMETER。
- bizContent.merchantOrderNo 长度边界 String(64)；缺失或非法返回 INVALID_PARAMETER。
- 不存在的 merchantOrderNo 返回 62004 MERCHANT_ORDER_NO_NOT_EXIST。
- requestTime 时间窗校验：过早返回 REQUESTTIME_TOO_EARLY；过晚返回 REQUESTTIME_TOO_LATER。
- 频控：高频调用返回 402 RATE_LIMIT_REJECT。
- 授权：未授权商户/未签约 transfer 产品返回 403 UNAUTHORIZED；产品未开通场景与 placeTransferToBankOrder 一致（此接口不返回 62026，但需确认链路一致）。
- 成功响应 head.code=0、msg=SUCCESS，body.transferToBankOrder.merchantOrderNo 与请求一致。
- 状态校验：创建后立即查询应能查到 status=CREATED；付款成功 status=SUCCESS 且 paymentInfo.arrivalTime、payerFeeAmount、bankReference、swiftCode 返回；失败 status=FAILURE；银行退票 status=BANK_FAIL。
- 敏感字段返回校验：holderName、iban、beneficiaryAddress 应为加密/脱敏字符串，与原值不同。
- 金额一致性：查询响应 amount{amount,currency} 与下单请求一致（currency 例 AED）。
- swiftCode 回显格式与下单一致（注意可能含空格如 "BBME AEAD"）。
- ResponseHeader 校验：applyStatus、code、msg、traceCode 字段齐全。
- 幂等查询：同一 merchantOrderNo 多次查询结果一致（状态推进除外）。
- 与异步通知 [[api_payby_transfer_to_bank_notify]] 结果对账一致。