---
id: api_payby_remove_save_card
object_type: API
domain: payby-open-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p15
tags:
- card
- unbind
- cardToken
subdomain: null
module: null
sensitivity: normal
name: 解绑卡接口
aliases:
- removeSaveCard
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
将已保存的 cardToken 置为失效，使该 cardToken 无法再被查询和使用。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/acquire2/removeSaveCard
- 生产URL: https://api.payby.com/sgs/api/acquire2/removeSaveCard
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
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 | |
| 业务内容 | bizContent | Required | CardIndexRequest | - | 业务内容 |

bizContent 字段：
- cardToken：需要解绑的已保存卡 token，例如 "M818494241569"

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 签名 | Sign | Required | String | |

### Http Body
body 字段仅在 applyStatus=SUCCESS 且 code=0 时返回。

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader | |
| 响应体 | body | Optional | Void | 解绑成功无业务返回 |

成功响应示例的 head：applyStatus=SUCCESS，code=0，msg=SUCCESS，success=true，traceCode 透传。

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
| 62078 | CARD_NOT_EXIST | cardToken填写错误或者卡已解绑 | 调整请求参数 |

## 测试校验点
- Header 必填项校验：缺失 Sign / Partner-Id 时应被拒绝；签名错误返回鉴权类错误。
- requestTime 时间窗口校验：过早返回 REQUESTTIME_TOO_EARLY，过晚返回 REQUESTTIME_TOO_LATER。
- bizContent.cardToken 必填校验：缺失或为空返回 400 INVALID_PARAMETER。
- 解绑有效 cardToken：返回 code=0，head.applyStatus=SUCCESS，body 为空（Void）。
- 重复解绑同一 cardToken：第二次应返回 62078 CARD_NOT_EXIST。
- 解绑后效果验证：用同一 cardToken 调用 [[api_payby_get_save_card]] 查询卡信息，应返回 62078 CARD_NOT_EXIST；用该 cardToken 发起后续支付应不可用。
- 不存在的 cardToken：返回 62078 CARD_NOT_EXIST。
- 限流场景：高频调用触发 402 RATE_LIMIT_REJECT。
- 未授权商户调用：返回 403 UNAUTHORIZED。
- 风控拦截：返回 601 RISK_FAIL。
- 跨商户解绑越权校验：商户 A 不应能解绑属于商户 B 的 cardToken（按业务规则应返回错误，参考 CARD_NOT_EXIST 或鉴权失败）。
- 响应签名校验：响应 Header 的 Sign 校验通过。
