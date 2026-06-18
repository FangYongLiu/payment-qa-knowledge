---
id: api_payby_get_transfer_to_bank_order
object_type: API
domain: payby-transfer-to-bank
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p3
tags:
- transfer
- query
- bank
subdomain: null
module: null
sensitivity: normal
name: 查询单笔付款到银行卡接口
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
用于单笔付款到银行卡的结果查询，返回付款的详细结果。当订单状态不明或未收到 PayBy 异步通知时，建议商户主动调用本接口确认订单状态。

## 路径/方法
- 联调 URL: https://uat.test2pay.com/sgs/api/transfer/getTransferToBankOrder
- 生产 URL: https://api.payby.com/sgs/api/transfer/getTransferToBankOrder
- 协议：HTTP POST，Content-Type: application/json

## 入参
Http Header：
- Content-Language Optional String(10)，例 en（en-英文）
- Sign Required String，签名
- Partner-Id Required String(12)，商户号

Http Body：
- requestTime Required Timestamp(3)，请求时间，例 1581493898000
- bizContent Required GetTransferToBankOrderRequest，业务内容

GetTransferToBankOrderRequest：
- merchantOrderNo Required String(64)，商户订单号，例 Me23484

## 出参
Http Header：
- Content-Language Optional String(10)
- Sign Required String
- Partner-Id Required String(12)

Http Body：
- head Required ResponseHeader（含 applyStatus、code、msg、traceCode）
- body Optional GetTransferToBankOrderResponse

GetTransferToBankOrderResponse：
- transferToBankOrder Required TransferToBankOrder

TransferToBankOrder（响应样例字段）：
- amount {amount, currency}
- holderName（加密）
- iban（加密）
- beneficiaryAddress（加密）
- memo
- merchantOrderNo
- notifyUrl
- orderNo
- paymentInfo {arrivalTime, payerFeeAmount{amount, currency}}
- product，例 "Transfer To Bank"
- requestTime
- status，例 SUCCESS
- swiftCode
- bankReference

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
- Header 必填校验：缺失 Sign / Partner-Id 应拒绝；Content-Language 可选。
- 签名校验：使用商户私钥签名，PayBy 公钥验签；篡改 body 应导致验签失败。
- requestTime 时间窗校验：过早返回 REQUESTTIME_TOO_EARLY；过晚返回 REQUESTTIME_TOO_LATER。
- bizContent.merchantOrderNo 必填、长度 ≤64；缺失或非法返回 INVALID_PARAMETER。
- 不存在的 merchantOrderNo 返回 62004 MERCHANT_ORDER_NO_NOT_EXIST。
- 高频调用返回 402 RATE_LIMIT_REJECT。
- 成功响应 head.code=0、msg=SUCCESS，body.transferToBankOrder.merchantOrderNo 与请求一致。
- 返回的 holderName / iban / beneficiaryAddress 为加密形态，与原值不同。
- 状态字段 status 与底层订单实际状态一致（如 SUCCESS）；paymentInfo.arrivalTime、bankReference、swiftCode 在成功时存在。
- 金额结构 amount{amount,currency} 与下单一致，currency 例 AED。
- 与异步通知 [[api_payby_transfer_to_bank_notify]] 结果对账一致。
