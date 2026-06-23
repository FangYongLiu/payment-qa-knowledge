---
id: api_payby_transfer_get_iban_holder_name
object_type: API
domain: fund-out-transfer
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki_attachment
source_ref: wiki_attachment:56e8e18c-82c1-4231-b586-2130e089c7da
tags:
- IBAN
- 姓名校验
- 转账
subdomain: null
module: null
sensitivity: normal
name: 查询IBAN姓名接口
aliases:
- getIbanHolderName
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
校验用户名称和IBAN账号是否匹配 / Verify whether the account name matches the IBAN number。商户在发起转账前可调用此接口预校验受益人姓名与 IBAN 是否匹配,降低出款失败风险。(since v2.2)

## 路径/方法
- 联调 URL: `https://uat.test2pay.com/sgs/api/transfer/getIbanHolderName`
- 生产 URL: `https://api.payby.com/sgs/api/transfer/getIbanHolderName`
- 提交方式: POST
- 传输方式: HTTPS
- 数据格式: JSON
- 字符编码: UTF-8
- 签名算法: SHA256WithRSA (请求与响应都需签名)

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
| 业务内容 | bizContent | Required | GetIbanHolderNameRequest | - | 业务内容 |

### GetIbanHolderNameRequest
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| Holder name | holderName | Required | String(256) | 加密传输 (RSA 公钥加密 + Base64) |
| IBAN | iban | Required | String(256) | 加密传输 (RSA 公钥加密 + Base64) |

> 加密说明: holderName / iban 使用 PayBy 颁发的 RSA 公钥加密,加密原文 UTF-8 编码,加密结果 Base64 编码,加密字段一般不超过 200 字节。

## 出参

### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader | |
| 响应体 | body | Optional | GetIbanHolderNameResponse | |

### GetIbanHolderNameResponse
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 订单信息 | ibanHolderName | Required | IbanHolderName | |

### IbanHolderName
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 受益人掩码 | holderNameMask | Optional | String(64) | xxx*** xxx*** xxx*** | |
| 名字比对等级 | nameMatchingLevel | Optional | String(32) | 1 | 1 - First name verification; 2 - First name and last name verification; 3 - Full name verification |
| 名字比对结果 | nameMatchingResult | Required | String | TRUE / FALSE | |

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
| 62101 | WRONG_IBAN_FORMAT | 传入的IBAN格式不对 | 调整 iban |
| 62102 | NAME_NOT_FOUND | 无法通过IBAN查询姓名 | 调整 iban |
| 62103 | QUERY_API_UNAVAILABLE | 查询接口不可用 | 稍后重试 |

## 测试校验点
- 请求头校验: Content-Language(可选)、Sign(必填,SHA256WithRSA 签名,Base64)、Partner-Id(必填,12 位)、Content-Type=application/json。
- 签名校验: 签名原文为请求 Http Body 原始内容,UTF-8 编码;响应签名亦需验签。
- 加密字段校验: holderName、iban 必须为 RSA 公钥加密 + Base64 后的密文,长度 ≤ String(256);明文 UTF-8 编码,加密前一般不超过 200 字节。
- 必填校验: requestTime、bizContent.holderName、bizContent.iban 缺失或为空 → 返回 400 INVALID_PARAMETER (空值不予处理)。
- requestTime 时效性: 远早于服务器当前时间 → 400 REQUESTTIME_TOO_EARLY;远晚于服务器当前时间 → 400 REQUESTTIME_TOO_LATER。
- IBAN 格式校验: 错误格式 → 62101 WRONG_IBAN_FORMAT。
- 姓名查询: 该 IBAN 在通道侧无法查询到姓名 → 62102 NAME_NOT_FOUND;通道查询接口不可用 → 62103 QUERY_API_UNAVAILABLE,需可重试。
- 频控: 高频请求 → 402 RATE_LIMIT_REJECT。
- 授权与服务可用性: 未授权 → 403 UNAUTHORIZED;服务不可用 → 404 SERVICE_NOT_AVAILABLE;系统错误 → 500 SYSTEM_ERROR;
