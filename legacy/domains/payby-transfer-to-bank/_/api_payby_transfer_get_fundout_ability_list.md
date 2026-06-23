---
id: api_payby_transfer_get_fundout_ability_list
object_type: API
domain: fund-out-transfer
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki_attachment
source_ref: wiki_attachment:56e8e18c-82c1-4231-b586-2130e089c7da
tags:
- transfer
- fundout
- ability
subdomain: null
module: null
sensitivity: normal
name: 查询出款能力接口
aliases:
- getFundoutAbilityList
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
查询商户可出款的国家、币种、网络与受益人类型组合能力清单(since v2.1)。商户在发起转账到银行前可调用此接口获取支持的出款能力。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/transfer/getFundoutAbilityList
- 生产URL: https://api.payby.com/sgs/api/transfer/getFundoutAbilityList
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
| 签名 | sign | Required | String | | |
| 商户号 | Partner-Id | Required | String(12) | | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 | |

请求样例 Http Body:
```json
{
    "requestTime": 1585142880000
}
```

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
| 响应体 | body | Optional | GetFundoutAbilityListResponse | - | |

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

响应样例(节选):
```json
{
  "head": {"applyStatus":"SUCCESS","code":"0","msg":"SUCCESS","traceCode":"0837"},
  "body": {
    "fundoutAbilityList":[
      {"beneficiaryType":"IBAN","name":"Local","networkCode":"LOCAL","countryCode":"UAE","fundoutCurrencyCode":"AED"},
      {"beneficiaryType":"IBAN","name":"Local","networkCode":"LOCAL","countryCode":"UAE","fundoutCurrencyCode":"USD"},
      {"beneficiaryType":"BBAN","name":"SWIFT","networkCode":"SWIFT","countryCode":"HK","fundoutCurrencyCode":"USD"},
      {"beneficiaryType":"BBAN","name":"SWIFT","networkCode":"SWIFT","countryCode":"SG","fundoutCurrencyCode":"USD"},
      {"beneficiaryType":"BBAN","name":"SWIFT","networkCode":"SWIFT","countryCode":"US","fundoutCurrencyCode":"USD"}
    ]
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

## 测试校验点
- HTTPS + POST + JSON + UTF-8;请求/响应均需 SHA256WithRSA 签名,签名结果 Base64 编码。
- Http Header 必传 sign、Partner-Id;Content-Language 可选(en)。
- Http Body 必传 requestTime(Timestamp(3));requestTime 过早/过晚应分别返回 400 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER。
- 空值参数不予处理(请求参数规则)。
- 商户未授权时返回 403 UNAUTHORIZED;频繁调用返回 402 RATE_LIMIT_REJECT。
- 响应 head.applyStatus 为 SUCCESS/FAIL/ERROR,code=0 时表示成功。
- 响应 body.fundoutAbilityList 为 List<FundoutAbility>,每条记录包含 beneficiaryType、countryCode、fundoutCurrencyCode、name、networkCode 五个必填字段。
- 校验 beneficiaryType 取值范围(IBAN/BBAN/FED_WIRE)、networkCode 取值范围(SWIFT/LOCAL)、fundoutCurrencyCode 与 countryCode 组合是否符合商户配置。
- 验证签名错误、Partner-Id 缺失/错误等异常场景返回的错误码与文案。
