---
id: api_payby_update_expired_time
object_type: API
domain: payby-open-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p16
tags:
- acquire
- order
- expired-time
subdomain: acquire2
module: null
sensitivity: normal
name: 更新订单超时时间接口
aliases:
- updateExpiredTime
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
调整订单过期时间，过期时间只能为调用接口时间往后的15天内。

## 路径/方法
- 联调URL: `https://uat.test2pay.com/sgs/api/acquire2/updateExpiredTime`
- 生产URL: `https://api.payby.com/sgs/api/acquire2/updateExpiredTime`
- 方法: HTTP POST (JSON)

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
| 业务内容 | bizContent | Required | UpdateExpiredTimeRequest | - |

### bizContent (UpdateExpiredTimeRequest)
- `merchantOrderNo`：商户订单号，例如 `M965739182419`
- `expiredTime`：新的过期时间，Timestamp(3)，例如 `1581412155966`，必须在调用接口时间往后 15 天内

## 出参

### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | sign | Required | String |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader | |
| 响应体 | body | Optional | GetOrderResponse | 仅当 applyStatus=SUCCESS 且 code=0 时返回 |

### GetOrderResponse
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 订单信息 | acquireOrder | Required | AcquireOrder |

AcquireOrder 关键字段（见响应样例）：`merchantOrderNo`、`orderNo`、`status`(如 SETTLED)、`reserved`、`paymentInfo`(paidAmount、paidTime、payerMid、payeeFeeAmount、payerFeeAmount、payChannel)、`product`、`totalAmount`、`payeeMid`、`expiredTime`、`notifyUrl`、`subject`、`requestTime`、`accessoryContent`(amountDetail/goodsDetail/terminalDetail)、`paySceneCode`、`revoked`。

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
| 62089 | INVALID_EXPIRED_TIME | 无效的超时时间 | 调整请求参数 |

## 测试校验点
- Header 必填校验：`Sign`、`Partner-Id` 缺失或错误时鉴权失败（403 UNAUTHORIZED）。
- `Content-Language` 可选，不传时验证默认行为；传 `en` 时返回英文文案。
- `requestTime` 偏离当前时间过多分别返回 `REQUESTTIME_TOO_EARLY` / `REQUESTTIME_TOO_LATER`。
- `merchantOrderNo` 必填且需对应已存在订单；不存在或非法返回 `INVALID_PARAMETER`。
- `expiredTime` 边界校验：
  - 早于当前时间 → `INVALID_EXPIRED_TIME` (62089)
  - 晚于当前时间 + 15 天 → `INVALID_EXPIRED_TIME` (62089)
  - 在当前时间到 +15 天范围内 → 成功，返回 acquireOrder.expiredTime 等于入参 `expiredTime`。
- 成功响应 `head.applyStatus=SUCCESS`、`code=0`，且 `body` 字段返回；其他情况 `body` 不返回。
- 返回的 `acquireOrder.expiredTime` 与请求 `expiredTime` 一致；其他字段（status、paymentInfo、totalAmount 等）保持原订单数据。
- 高频调用触发 `RATE_LIMIT_REJECT` (402)。
- 风控拦截场景返回 `RISK_FAIL` (601)。
- 服务异常/超时分别返回 `SYSTEM_ERROR` (500) 与 `SERVICE_TIMEOUT` (504)。
- 响应 Header `sign` 验签通过。
