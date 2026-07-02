---
id: api_transfer_get_iban_holder_name
object_type: API
domain: wallet
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p1
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
related_services:
- svc_transfer
---

## 用途
校验用户名称和IBAN账号是否匹配 / Verify whether the account name matches the IBAN number.

## 路径/方法
- 联调URL: `https://uat.test2pay.com/sgs/api/transfer/getIbanHolderName`
- 生产URL: `https://api.payby.com/sgs/api/transfer/getIbanHolderName`
- 提交方式: POST
- 数据格式: JSON
- 传输: HTTPS
- 字符编码: UTF-8
- 签名算法: SHA256WithRSA
- since: v2.2 (2024-08-20)

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
| 请求时间 | requestTime | Required | Timestamp(3) | |
| 业务内容 | bizContent | Required | GetIbanHolderNameRequest | |

### GetIbanHolderNameRequest
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| Holder name | holderName | Required | String(256) | 加密传输（RSA公钥加密，Base64编码） |
| IBAN | iban | Required | String(256) | 加密传输（RSA公钥加密，Base64编码） |

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
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 受益人掩码 | holderNameMask | Optional | String(64) | 例: `xxx*** xxx*** xxx***` |
| 名字比对等级 | nameMatchingLevel | Optional | String(32) | 1 - First name verification；2 - First name and last name verification；3 - Full name verification |
| 名字比对结果 | nameMatchingResult | Required | String | TRUE/FALSE |

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
| 62101 | WRONG_IBAN_FORMAT | 传入的IBAN格式不对 | 调整iban |
| 62102 | NAME_NOT_FOUND | 无法通过IBAN查询姓名 | 调整iban |
| 62103 | QUERY_API_UNAVAILABLE | 查询接口不可用 | 稍后重试 |

## 测试校验点
- 请求必须使用 HTTPS + POST + JSON + UTF-8。
- Header 必须包含 `Sign`、`Partner-Id`；签名为请求 Http Body 原始内容的 SHA256WithRSA 签名，Base64 编码。
- `holderName` 与 `iban` 必须使用 PayBy 颁发的 RSA 公钥加密并 Base64 编码后传输；加密原文不超过 200 字节。
- `requestTime` 偏离当前时间过多会返回 `REQUESTTIME_TOO_EARLY` / `REQUESTTIME_TOO_LATER`。
- 入参缺失或格式非法 → `INVALID_PARAMETER`；IBAN 格式错误 → `WRONG_IBAN_FORMAT (62101)`。
- 通过 IBAN 查不到姓名 → `NAME_NOT_FOUND (62102)`；上游查询接口不可用 → `QUERY_API_UNAVAILABLE (62103)`。
- 高频调用触发 `RATE_LIMIT_REJECT (402)`。
- 成功响应 `head.applyStatus=SUCCESS`、`code=0`，`body.ibanHolderName.nameMatchingResult` 仅为 `TRUE` 或 `FALSE`。
- `nameMatchingLevel` 取值范围 {1,2,3}，分别对应 First name / First+Last name / Full name 校验。
- `holderNameMask` 应为掩码格式，不泄露完整姓名。
- 响应需校验返回 Header 中的 `Sign`（响应数据也需签名）。
