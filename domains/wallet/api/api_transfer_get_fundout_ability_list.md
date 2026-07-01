---
id: api_transfer_get_fundout_ability_list
object_type: API
domain: wallet
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p1
tags:
- transfer
- fundout
- ability
- since-v2.1
subdomain: null
module: null
sensitivity: normal
name: 查询出款能力接口
aliases:
- getFundoutAbilityList
related_services:
- svc_transfer
---

## 用途
查询商户可出款到的国家、币种、网络等出款能力列表（since v2.1）。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/transfer/getFundoutAbilityList
- 生产URL: https://api.payby.com/sgs/api/transfer/getFundoutAbilityList
- 提交方式: POST
- 传输方式: HTTPS
- 数据格式: JSON
- 字符编码: UTF-8

## 入参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en | en-英文 |
| 签名 | sign | Required | String | | SHA256WithRSA |
| 商户号 | Partner-Id | Required | String(12) | | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 | |

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en | en-英文 |
| 签名 | Sign | Required | String | | |
| 商户号 | Partner-Id | Required | String(12) | | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader | |
| 响应体 | body | Optional | GetFundoutAbilityListResponse | |

### GetFundoutAbilityListResponse
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 出款能力列表 | fundoutAbilityList | Required | List<FundoutAbility> | |

### FundoutAbility
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 收益人类型 | beneficiaryType | Required | String(20) | IBAN | IBAN / BBAN / FED_WIRE |
| 国家代码 | countryCode | Required | String(20) | UAE | |
| 到账币种 | fundoutCurrencyCode | Required | String(20) | USD | USD / AED |
| 收益人名称 | name | Required | String(20) | Local | |
| 网络代码 | networkCode | Required | String(20) | SWIFT | SWIFT / LOCAL |

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

## 测试校验点
- 必填头校验：Partner-Id、sign 必传；缺失或签名错误应授权失败。
- 请求体仅含 requestTime（Timestamp(3)），异常时间需返回 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER。
- 响应签名校验：使用 PayBy 公钥校验响应 sign。
- 响应 head.applyStatus = SUCCESS、code = 0 时，body.fundoutAbilityList 应非空。
- FundoutAbility 字段枚举校验：
  - beneficiaryType ∈ {IBAN, BBAN, FED_WIRE}
  - networkCode ∈ {SWIFT, LOCAL}
  - fundoutCurrencyCode 含 USD / AED 等
- 不同 (countryCode, networkCode, fundoutCurrencyCode, beneficiaryType) 组合的能力条目应去重且与商户配置一致。
- 高频调用应触发 RATE_LIMIT_REJECT (402)。
- 未授权商户调用应返回 UNAUTHORIZED (403)。
- 服务不可用 / 超时 / 系统异常分别返回 404 / 504 / 500。
