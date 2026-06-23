---
id: api_payby_revoke_order
object_type: API
domain: payby-open-api
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p15
tags:
- 冲正
- 退款
- 订单关闭
subdomain: null
module: null
sensitivity: normal
name: 订单冲正接口
aliases:
- revokeOrder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当商户认为可能交易失败时采取的补救手法。商户发送到PayBy的收单交易未得到响应、不确定是否成功完成时，向PayBy发起冲正请求：若PayBy端已支付成功则发起退款，否则关闭未支付订单。

特性：
- 不提供冲正查询接口，冲正结果通过查询订单获得，订单上新增冲正标志 `revoked`（true=已冲正，false=未冲正）。
- 冲正过程不可查询（如退款进度）。
- 已结算订单状态不再变更，即使被冲正，冲正通过退款订单来反映。
- 未支付订单冲正后，订单会被置成 `FAILURE`。

## 路径/方法
- 联调URL：https://uat.test2pay.com/sgs/api/acquire2/revokeOrder
- 生产URL：https://api.payby.com/sgs/api/acquire2/revokeOrder
- 方法：HTTP POST，Content-Type: application/json

## 入参
Http Header
- Content-Language Optional String(10)：文案语言，如 en
- Sign Required String：签名
- Partner-Id Required String(12)：商户号

Http Body
- requestTime Required Timestamp(3)：请求时间，如 1581493898000
- bizContent Required OrderIndexRequest：业务内容
  - merchantOrderNo：商户订单号（请求样例中使用）

## 出参
Http Header
- Content-Language Optional String(10)
- Sign Required String
- Partner-Id Required String(12)

Http Body
- head Required ResponseHeader：含 applyStatus、code、msg
- body Optional RevokeOrderResponse：仅在 applyStatus=SUCCESS 且 code=0 时返回

RevokeOrderResponse
- acquireOrder Required AcquireOrder：订单信息
  - 新增字段 `revoked`：true=已冲正，false=未冲正
  - 未支付订单冲正后 `status` 为 `FAILURE`
  - 其它字段：merchantOrderNo、orderNo、status、paymentInfo（paidAmount/paidTime/payerMid/payeeFeeAmount/payerFeeAmount/payChannel）、product、totalAmount、payeeMid、expiredTime、notifyUrl、subject、requestTime、accessoryContent、paySceneCode 等

## 错误码
| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |
| 62035 | ORDER_NO_NOT_EXIST | PayBy订单号的订单不存在 | 调整PayBy订单号 |
| 62039 | REVOKE_FAILURE | PayBy内部错误 | 联系PayBy |
| 62041 | ACQUIRE_ORDER_REFUNDED | 收单订单已退款 | 调整商户订单号 |
| 62046 | REVOKE_REJECTED | 冲正已拒绝 | 请调整业务 |

## 测试校验点
- Header 必填项校验：Sign、Partner-Id 缺失或错误返回 403 UNAUTHORIZED 或 400。
- Body 必填项校验：requestTime、bizContent.merchantOrderNo 缺失返回 400 INVALID_PARAMETER。
- requestTime 偏离当前时间过早/过晚分别触发 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER。
- merchantOrderNo 不存在：返回 62004 MERCHANT_ORDER_NO_NOT_EXIST。
- 订单已退款场景：返回 62041 ACQUIRE_ORDER_REFUNDED。
- 冲正被拒：返回 62046 REVOKE_REJECTED。
- 内部错误：返回 62039 REVOKE_FAILURE。
- 成功冲正后查询订单：
  - 已支付订单：通过退款订单反映，原订单状态保持已结算不变更，`revoked=true`。
  - 未支付订单：订单 `status` 变更为 `FAILURE`，`revoked=true`。
- 不存在冲正查询接口，冲正结果只能通过订单查询接口获得 `revoked` 标志判断。
- 风控拒绝：返回 601 RISK_FAIL。
- 频控：高频请求返回 402 RATE_LIMIT_REJECT。
- 响应在 applyStatus=SUCCESS 且 code=0 时才返回 body.acquireOrder，否则 body 不返回。
