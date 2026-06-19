---
id: api_payby_get_cashier_url_info
object_type: API
domain: payby-open-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p15
tags:
- 收银台
- 二维码
- 脱敏
subdomain: null
module: null
sensitivity: normal
name: 查询收银台URL信息接口
aliases:
- getCashierUrlInfo
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
This interface returns whether the QR code has been scanned by the user, and information about the scanner (mask)。即查询收银台二维码是否被用户扫描，以及扫描者的脱敏信息。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/acquire2/getCashierUrlInfo
- 生产URL: https://api.payby.com/sgs/api/acquire2/getCashierUrlInfo
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
| 请求时间 | requestTime | Required | Timestamp(3) | 示例 1581493898000 |
| 业务内容 | bizContent | Required | GetCashierUrlInfoRequest | 业务内容 |

### GetCashierUrlInfoRequest
- tokenUrl：收银台 URL，例如 `https://checkout.payby.com/pay-page/main?BIZ_TYPE=202&ft=xxx&t=xxx`

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | Sign | Required | String |

### Http Body
Http Body 里的 body 字段在 applyStatus 为 SUCCESS 并且 code 为 0 的时候才返回。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | GetCashierUrlInfoResponse |

### GetCashierUrlInfoResponse
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 付款人信息 | payer | Required | Payer |

### Payer（响应样例字段）
- mobileNumberMask：付款人手机号脱敏，示例 `+971-58*****92`

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
| 62082 | TOKEN_URL_NOT_EXIST | tokenUrl错误或者已失效 | 调整请求参数 |

## 测试校验点
- Header 必填校验：Sign、Partner-Id 缺失或错误时应返回 UNAUTHORIZED(403)/INVALID_PARAMETER(400)。
- requestTime 时间窗校验：过早返回 REQUESTTIME_TOO_EARLY，过晚返回 REQUESTTIME_TOO_LATER。
- bizContent.tokenUrl 必填且有效：缺失返回 INVALID_PARAMETER(400)；错误或已失效返回 62082 TOKEN_URL_NOT_EXIST。
- 二维码未被扫描场景：验证 body 字段是否返回（仅在 applyStatus=SUCCESS 且 code=0 时返回 body），未扫描时 payer 信息的取值规则。
- 二维码已被扫描场景：验证 payer.mobileNumberMask 返回脱敏格式（如 `+971-58*****92`），未泄露完整手机号。
- 频控校验：高频请求触发 RATE_LIMIT_REJECT(402)。
- 风控校验：触发风控时返回 RISK_FAIL(601)。
- 系统异常：构造系统/超时场景，分别返回 SYSTEM_ERROR(500)、SERVICE_TIMEOUT(504)、SERVICE_NOT_AVAILABLE(404)。
- 签名验证：响应 Header 的 Sign 应可被验签。
- 仅当 applyStatus=SUCCESS 且 code=0 时 body 才返回，其他情况 body 应为空。
