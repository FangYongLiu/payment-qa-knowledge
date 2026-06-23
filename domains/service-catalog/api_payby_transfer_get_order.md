---
id: api_payby_transfer_get_order
object_type: API
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p13
tags:
- 查询
- 付款到账户
- Transfer
subdomain: null
module: null
sensitivity: normal
name: 查询单笔付款到账户订单接口
aliases:
- getTransferOrder
related_services:
- svc_transfer
---

## 用途
用于单笔付款到账户的结果查询，返回付款的详细结果。配合 [[api_payby_transfer_place_order]] 单笔付款到账户下单接口使用，业务背景见 [[payby-transfer-to-account]]。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/transfer/getTransferOrder
- 生产URL: https://api.payby.com/sgs/api/transfer/getTransferOrder
- 方法: HTTP POST (Content-Type: application/json)

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
| 请求时间 | requestTime | Required | Timestamp(3) | |
| 业务内容 | bizContent | Required | GetTransferOrderRequest | 业务内容 |

### GetTransferOrderRequest
| 字段名 | 变量名 | 必填 | 类型 | 示例 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | Me23484 | |

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | sign | Required | String |

### Http Body
- head: ResponseHeader (Required)
- body: GetTransferOrderResponse (Optional，仅当 applyStatus=SUCCESS 且 code=0 时返回)

### GetTransferOrderResponse
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 订单信息 | transferOrder | Required | TransferOrder | 付款到账户订单信息 |

### TransferOrder 关键字段（响应样例）
- amount: Money (currency, amount)
- beneficiaryFullName: String（加密）
- beneficiaryIdentity: String（加密）
- memo: String
- merchantOrderNo: String
- notifyUrl: String
- orderNo: String
- paymentInfo: { arrivalTime, payerFeeAmount }
- product: 固定值 "Transfer"
- requestTime: Timestamp
- status: CREATED / SUCCESS / FAILURE

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
- Header 必填项校验：Sign、Partner-Id 缺失或错误时鉴权/签名失败（UNAUTHORIZED / INVALID_PARAMETER）。
- requestTime 边界：过早/过晚分别返回 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER。
- merchantOrderNo 必填：缺失返回 INVALID_PARAMETER；不存在的订单号返回 62004 MERCHANT_ORDER_NO_NOT_EXIST。
- 仅在 applyStatus=SUCCESS 且 code=0 时返回 body.transferOrder，其他情况 body 不返回。
- 响应 transferOrder.status 应为状态机三态之一：CREATED / SUCCESS / FAILURE，与下单接口 [[api_payby_transfer_place_order]] 创建后的实际状态一致。
- 响应中 beneficiaryFullName、beneficiaryIdentity 应为加密字段，保持与下单时一致。
- product 固定为 "Transfer"；orderNo 与下单返回值一致；paymentInfo.arrivalTime、payerFeeAmount 应正确返回。
- 限流场景：高频查询触发 402 RATE_LIMIT_REJECT。
- 签名校验：响应 Header 中 sign 必返回且需校验通过。
