---
id: api_payby_get_protocol
object_type: API
domain: payby-authorization-protocol
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-auth-agreement-v1.0.2-p1
tags:
- protocol
- query
- POST
subdomain: null
module: null
sensitivity: normal
name: 查询协议
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures:
- payby-auth-protocol-return-codes
---

## 用途
提供 PayBy 协议查询能力，商户可通过商户订单号主动查询签约协议状态与详情，用于以下情况：
1. 商户后台、网络、服务器等出现异常，未接收到协议结果通知；
2. 商户需要查询用户签订的协议号。

## 路径/方法
- 提交方式：POST
- 数据格式：JSON，UTF-8
- 传输方式：HTTPS
- 联调URL: https://uat.test2pay.com/sgs/api/protocol/getProtocol
- 生产URL: https://api.payby.com/sgs/api/protocol/getProtocol

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
| 业务内容 | bizContent | Required | GetProtocolRequest | |

### GetProtocolRequest
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | |

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | sign | Required | String |

### Http Body
body 字段仅在 applyStatus=SUCCESS 且 code=0 时返回。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | GetProtocolResponse |

### ResponseHeader
| 字段 | 变量名 | 类型 | 描述 |
| --- | --- | --- | --- |
| 请求状态 | applyStatus | String(16) | SUCCESS / FAIL / ERROR |
| 返回错误码 | code | String(10) | |
| 返回信息 | msg | String(200) | |

### GetProtocolResponse
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 订单信息 | protocol | Required | Protocol |

### Protocol
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | |
| PayBy协议号 | authProtocolNo | Optional | String(32) | |
| 申请签约状态 | applySignStatus | Required | String(32) | APPLYING/CLOSED/SIGNED/FAILURE |
| 签约时间 | signTime | Optional | Timestamp(3) | |
| 生效时间 | effectTime | Optional | Timestamp(3) | |
| 失效时间 | invalidTime | Optional | Timestamp(3) | |
| 协议状态 | protocolStatus | Optional | String(32) | EXPIRED/TERMINATED/EFFECTIVE/INEFFECTIVE |
| 签约人ID | signerId | Optional | String(32) | 签约人在PayBy的会员ID |
| 扣除类型 | deductType | Optional | String(32) | SP=Single Pay Method |
| 扩展信息 | extension | Optional | Map<String,String> | 包含 payMethodType(BALANCE/CARD_PAY)、lastFour、cardBrand |

## 错误码
| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系ToPay |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系ToPay |
| 500 | SYSTEM_ERROR | 系统错误 | 联系ToPay,稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |
| 90005 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |

## 测试校验点
- 请求必须使用 HTTPS + POST + JSON + UTF-8；签名算法 SHA256WithRSA，请求与响应均需签名校验。
- Http Header：Sign、Partner-Id 必填；Content-Language 可选(en)。
- Http Body：requestTime 必填，bizContent.merchantOrderNo 必填(String(64))；空值参数不予处理。
- 当传入不存在的 merchantOrderNo 时返回 90005 MERCHANT_ORDER_NO_NOT_EXIST。
- requestTime 偏离当前时间过早/过晚时返回 400 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER。
- 高频请求触发 402 RATE_LIMIT_REJECT。
- 仅在 applyStatus=SUCCESS 且 code=0 时返回 body.protocol，其它状态 body 不返回。
- 校验返回 protocol.applySignStatus 取值范围(APPLYING/CLOSED/SIGNED/FAILURE)、protocolStatus 取值范围(EXPIRED/TERMINATED/EFFECTIVE/INEFFECTIVE)。
- 校验 signTime/effectTime/invalidTime 为 Timestamp(3) 毫秒时间戳。
- 校验扩展字段 deductType=SP，extension 中 payMethodType、lastFour、cardBrand 的取值(VISA/MASTERCARD/CUP/JCB/DINERS/MAESTRO/AE/EBT/DISCOVER/CIRRUS/RUPAY/UATP/ELO)。
- 用于异常补偿场景：未收到 [[api_payby_protocol_notify]] 通
