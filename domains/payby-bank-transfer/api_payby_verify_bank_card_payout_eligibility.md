---
id: api_payby_verify_bank_card_payout_eligibility
object_type: API
domain: fund-out-transfer
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-bankcard-v0.2-p1
tags:
- bank-card
- verify
- payout
subdomain: null
module: null
sensitivity: normal
name: 验证银行卡支付资格接口
aliases:
- verifyBankCardPayoutEligibility
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
验证银行卡是否符合支付（转账到银行卡）条件，返回该卡支持的 payout 类型（CardPayoutsType）。

## 路径/方法
- 联调URL: `https://uat.test2pay.com/sgs/api/transfer/verifyBankCardPayoutEligibility`
- 生产URL: `https://api.payby.com/sgs/api/transfer/verifyBankCardPayoutEligibility`
- 提交方式: POST
- 传输方式: HTTPS
- 数据格式: JSON
- 字符编码: UTF-8
- 签名算法: SHA256WithRSA

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
| 业务内容 | bizContent | Required | VerifyBankCardPayoutEligibilityRequest | - | 业务内容 |

### VerifyBankCardPayoutEligibilityRequest
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 卡号 | cardNumber | Optional | String(50) | - | 加密传输；长度 12~19；全部为数字字符 |
| 卡token | cardToken | Optional | String(32) | 11181726721657465380 | |
| cardTokenMerchantId | cardTokenMerchantId | Optional | String(32) | | |
| 卡号后4位 | last4 | Optional | String(4) | 0040 | cardToken 非空时，必输 |

## 出参

### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en | en-英文 |
| 签名 | Sign | Required | String | | |
| 商户号 | Partner-Id | Required | String(12) | | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader | - | |
| 响应体 | body | Optional | VerifyBankCardPayoutEligibilityResponse | - | |

### VerifyBankCardPayoutEligibilityResponse
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 订单信息 | cardPayoutsType | Required | CardPayoutsType | STANDARD | |

### CardPayoutsType 枚举
| 代码 | 说明 |
| --- | --- |
| UNKNOWN | 未知 |
| NOT_SUPPORTED | 不支持 |
| FAST_FUNDS | 快速资金 |
| STANDARD | 标准 |

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
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |
| 62103 | QUERY_API_UNAVAILABLE | 查询接口不可用 | 稍后重试 |
| 62105 | INVALID_DATA_SENT | Invalid data was sent to retrieve API | 调整请求参数 |

## 测试校验点
- Header 校验：Partner-Id、Sign 必填；Sign 为 SHA256WithRSA 对 Http Body 原文签名（Base64）。
- requestTime 必填，时间偏差过大返回 REQUESTTIME_TOO_EARLY/REQUESTTIME_TOO_LATER。
- bizContent 必填，且 cardNumber 加密传输（RSA + Base64），明文长度 12~19、纯数字。
- cardToken 与 cardNumber 入参组合校验：当 cardToken 非空时 last4 必输。
- cardTokenMerchantId 长度 ≤ 32。
- 响应 head.applyStatus 取值 SUCCESS/FAIL/ERROR；code=0 时 body.cardPayoutsType 必返回。
- cardPayoutsType 枚举值校验：UNKNOWN、NOT_SUPPORTED、FAST_FUNDS、STANDARD，不在枚举内视为异常。
- 高频请求触发 402 RATE_LIMIT_REJECT；未授权商户返回 403 UNAUTHORIZED。
- 参数缺失/格式错误返回 400 INVALID_PARAMETER 或 62105 INVALID_DATA_SENT。
- 风控拒绝返回 601 RISK_FAIL。
- 响应签名验签通过（使用 PayBy 公钥）。
