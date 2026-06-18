---
id: api_payby_get_save_card
object_type: API
domain: payby-acquire-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p15
tags:
- card
- query
- saved-card
subdomain: null
module: null
sensitivity: normal
name: 查询卡信息接口
aliases:
- getSaveCard
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
通过已保存的 cardToken 查询卡的展示信息（品牌、卡类型、末四位等），用于商户侧展示已保存的卡。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/acquire2/getSaveCard
- 生产URL: https://api.payby.com/sgs/api/acquire2/getSaveCard
- 方法: HTTP POST，Content-Type: application/json

## 入参
Http Header

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

Http Body

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 | |
| 业务内容 | bizContent | Required | CardIndexRequest | - | 业务内容 |

bizContent (CardIndexRequest)

| 字段名 | 必填 | 描述 |
| --- | --- | --- |
| cardToken | Required | 已保存卡的 token |

请求示例：
```json
{
  "requestTime": 1581406091642,
  "bizContent": {
    "cardToken": "M818494241569"
  }
}
```

## 出参
Http Header

| 变量名 | 必填 | 类型 |
| --- | --- | --- |
| Sign | Required | String |

Http Body（body 字段仅在 applyStatus=SUCCESS 且 code=0 时返回）

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | GetSaveCardResponse |

GetSaveCardResponse

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 订单信息 | cardInfo | Required | CardInfo |

CardInfo（依据响应样例）

| 变量名 | 描述 |
| --- | --- |
| brand | 卡品牌，如 MASTERCARD |
| cardToken | 卡 token |
| cardType | 卡类型，如 DC |
| last4 | 卡号末四位 |

响应示例：
```json
{
  "body": {
    "cardInfo": {
      "brand": "MASTERCARD",
      "cardToken": "11194330633016421841",
      "cardType": "DC",
      "last4": "0008"
    }
  },
  "head": {
    "applyStatus": "SUCCESS",
    "code": "0",
    "msg": "SUCCESS",
    "success": true,
    "traceCode": "831851"
  }
}
```

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
- Header 必填项校验：缺失 Sign / Partner-Id 应被拒绝；Content-Language 可选（en）。
- 签名校验：错误签名应返回 UNAUTHORIZED(403)；签名正确流程通过。
- requestTime 边界：过早/过晚分别返回 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER (400)。
- bizContent.cardToken 必填：缺失或格式错误返回 INVALID_PARAMETER(400)。
- cardToken 不存在或已解绑：返回 62078 CARD_NOT_EXIST。
- 成功响应校验：applyStatus=SUCCESS 且 code=0 时才返回 body；cardInfo 包含 brand、cardToken、cardType、last4 四个字段。
- last4 应为 4 位数字，cardToken 与请求保持一致性（用于核对）。
- 频控：高频调用应触发 RATE_LIMIT_REJECT(402)。
- 未授权商户调用：返回 UNAUTHORIZED(403)。
- 联调与生产环境 URL 区分校验，路径为 /sgs/api/acquire2/getSaveCard。
- 解绑后再次查询同一 cardToken 应返回 62078（与 [[api_payby_remove_save_card]] 联动验证）。
