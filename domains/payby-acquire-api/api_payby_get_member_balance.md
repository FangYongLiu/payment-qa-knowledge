---
id: api_payby_get_member_balance
object_type: API
domain: payby-open-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p16
tags:
- 余额查询
- 会员账户
subdomain: null
module: null
sensitivity: normal
name: 查询会员余额接口
aliases:
- getMemberBalance
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
This interface is used to query the member account balance. 用于按币种查询会员账户的可用余额(availableBalance)。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/member/getBalance
- 生产URL: https://api.payby.com/sgs/api/member/getBalance
- 方法: HTTP POST (application/json)

## 入参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 示例值 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 |
| 业务内容 | bizContent | Required | GetMemberBalanceRequest | - |

### GetMemberBalanceRequest
| 字段名 | 变量名 | 必填 | 类型 | 示例值 |
| --- | --- | --- | --- | --- |
| 币种 | currencyCode | Required | String | AED |

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | Sign | Required | String |

### Http Body
- body 字段仅在 applyStatus=SUCCESS 且 code=0 时返回。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | MemberBalance |

### MemberBalance
| 字段名 | 变量名 | 必填 | 类型 | 示例值 |
| --- | --- | --- | --- | --- |
| 会员ID | memberId | Required | String | 200000018128 |
| 订单信息 | balanceList | Required | List<Balance> | - |

### Balance
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 可用余额 | availableBalance | Required | Money |

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
| 78001 | CURRENCY_CODE_NOT_SUPPORTED | 币种不支持 | 调整请求参数 |

## 测试校验点
- Header 必填项校验：Sign、Partner-Id 缺失或错误时鉴权失败 (UNAUTHORIZED/签名校验)。
- bizContent.currencyCode 必填；传入不支持的币种应返回 78001 CURRENCY_CODE_NOT_SUPPORTED。
- requestTime 偏离当前时间过早/过晚分别返回 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER。
- 参数缺失或非法返回 400 INVALID_PARAMETER。
- 成功响应：head.applyStatus=SUCCESS 且 head.code=0 时才返回 body；校验 body.memberId 与请求商户/会员一致，balanceList 非空，每项 availableBalance.currency 与请求 currencyCode 一致，amount 数值与精度正确。
- 高频请求触发 402 RATE_LIMIT_REJECT。
- 风控拦截返回 601 RISK_FAIL。
- 服务不可用/超时分别返回 404 SERVICE_NOT_AVAILABLE / 504 SERVICE_TIMEOUT；系统错误返回 500 SYSTEM_ERROR。
- 响应 Header.sign 验签通过。
