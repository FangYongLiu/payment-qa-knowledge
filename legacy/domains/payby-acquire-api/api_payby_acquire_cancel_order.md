---
id: api_payby_acquire_cancel_order
object_type: API
domain: payby-open-api
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p11
tags:
- 取消订单
- 收单
- PayBy
subdomain: null
module: null
sensitivity: normal
name: 取消订单接口 (cancelOrder)
aliases:
- cancelOrder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
撤销未支付的 PayBy 收单订单，避免重复支付。典型场景：
1. 商户订单支付失败需生成新单号重新发起支付，需对原订单号订单取消，避免重复支付。
2. 系统下单后用户支付超时，系统退出不再受理，调用订单取消接口避免用户继续支付。

## 路径/方法
- 联调URL: `https://uat.test2pay.com/sgs/api/acquire2/cancelOrder`
- 生产URL: `https://api.payby.com/sgs/api/acquire2/cancelOrder`
- 方法: HTTP POST (JSON)

## 入参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 示例值 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 |
| 业务内容 | bizContent | Required | OrderIndexRequest | - |

bizContent 示例字段: `merchantOrderNo`(如 `M172475858661`)。

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | sign | Required | String |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader | |
| 响应体 | body | Optional | CancelOrderResponse | applyStatus=SUCCESS 且 code=0 时才返回 |

### CancelOrderResponse
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 订单信息 | acquireOrder | Required | AcquireOrder |

acquireOrder 关键字段: `merchantOrderNo`、`orderNo`、`status`(取消成功后为 `FAILURE`)、`product`、`totalAmount`、`payeeMid`、`expiredTime`、`notifyUrl`、`subject`、`requestTime`、`accessoryContent`(amountDetail/goodsDetail/terminalDetail)、`paySceneCode`。

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
| 62001 | ORDER_PAID | 订单已支付成功不支撤销 | 调整商户订单号 |
| 62002 | ORDER_FAILURE | 已失败的订单再次发起撤销 | 调整商户订单号 |
| 62003 | ORDER_SETTLED | 已结算的订单再次发起撤销 | 调整商户订单号 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |
| 62035 | ORDER_NO_NOT_EXIST | PayBy订单号的订单不存在 | 调整PayBy订单号 |

## 测试校验点
- 请求 Header: `sign`、`Partner-Id` 必填校验；`Content-Language` 可选(en)。
- Body: `requestTime` 为毫秒级 Timestamp(3)，过早/过晚分别返回 `REQUESTTIME_TOO_EARLY`/`REQUESTTIME_TOO_LATER`。
- `bizContent.merchantOrderNo` 必填，订单不存在返回 62004；若以 PayBy `orderNo` 查询不存在返回 62035。
- 订单状态校验：
  - 已支付订单撤销 → 62001 ORDER_PAID
  - 已失败订单再次撤销 → 62002 ORDER_FAILURE
  - 已结算订单撤销 → 62003 ORDER_SETTLED
- 取消成功后响应 `head.applyStatus=SUCCESS`、`code=0`，`acquireOrder.status` 变为 `FAILURE`。
- 仅 applyStatus=SUCCESS 且 code=0 时返回 body，其他情况无 body 字段。
- 响应 Header 包含 `sign`，需进行验签。
- 频控/未授权/服务不可用/系统错误/超时分别对应 402/403/404/500/504。
- 风控拦截返回 601 RISK_FAIL。
- 与 [[api_payby_acquire_get_order]] 配合：撤销前/后可通过 getOrder 查询确认订单状态及冲正(`revoked`)情况。
