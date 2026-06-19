---
id: api_payby_acquire_get_order
object_type: API
domain: payby-open-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p11
tags:
- 查询
- 订单状态
- 冲正
subdomain: null
module: null
sensitivity: normal
name: 查询订单接口 (getOrder)
aliases:
- getOrder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
提供所有PayBy订单的查询，商户可主动查询订单状态以驱动后续业务逻辑。适用场景：
1. 商户后台、网络、服务器等异常导致系统未接收到支付通知；
2. 调用支付接口后返回系统错误或未知交易状态；
3. 调用关单或撤销接口API之前确认支付状态；
4. 查询订单的冲正状态：当返回对象中 `acquireOrder.revoke` 为 true 时，判定该订单冲正成功。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/acquire2/getOrder
- 生产URL: https://api.payby.com/sgs/api/acquire2/getOrder
- 方法: HTTP POST (JSON)

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
| 请求时间 | requestTime | Required | Timestamp(3) | 1581450087000 | |
| 业务内容 | bizContent | Required | OrderIndexRequest | - | 业务内容 |

bizContent 示例字段：`merchantOrderNo`。

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | sign | Required | String |

### Http Body
注意：body 字段仅在 applyStatus 为 SUCCESS 且 code 为 0 时才返回。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | GetOrderResponse |

### GetOrderResponse
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 订单信息 | acquireOrder | Required | AcquireOrder |

AcquireOrder 关键字段（来自响应样例）：`merchantOrderNo`、`orderNo`、`status`(如 SETTLED)、`reserved`、`paymentInfo`(paidAmount/paidTime/payerMid/payeeFeeAmount/payerFeeAmount/payChannel)、`product`、`totalAmount`、`payeeMid`、`expiredTime`、`notifyUrl`、`subject`、`requestTime`、`accessoryContent`(amountDetail/goodsDetail/terminalDetail)、`paySceneCode`、`revoked`。

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
| 62035 | ORDER_NO_NOT_EXIST | PayBy订单号的订单不存在 | 调整PayBy订单号 |

## 测试校验点
- 请求 Header 必填：sign、Partner-Id；Content-Language 可选。
- 请求 Body 必填：requestTime（Timestamp(3)）、bizContent（含 merchantOrderNo）。
- 响应 body 仅在 applyStatus=SUCCESS 且 code=0 时返回，其他情况下不返回 body。
- 校验 acquireOrder.status 字段，覆盖如 SETTLED、FAILURE 等典型状态。
- 冲正状态判定：当 `acquireOrder.revoke` 为 true 时判定为冲正成功（注意响应样例中字段为 `revoked`）。
- requestTime 偏离当前时间过早/过晚需返回 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER。
- 不存在订单的查询：仅传 merchantOrderNo 不存在 → 62004；仅传 orderNo 不存在 → 62035。
- 高频调用应触发 402 RATE_LIMIT_REJECT。
- 未授权商户访问应返回 403 UNAUTHORIZED。
- 风控失败返回 601 RISK_FAIL。
- 验证响应签名 sign 正确性。
- 校验 paymentInfo 各字段（paidAmount/paidTime/payChannel 等）在已支付订单中存在且金额币种正确。
