---
id: api_payby_get_protocol
object_type: API
domain: payby-authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: upload:c28e6aeb-4485-4713-83f7-c926b25d5235
tags:
- protocol
- query
- payby
subdomain: null
module: null
sensitivity: normal
name: 查询协议接口
aliases:
- getProtocol
- 查询协议
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
提供PayBy协议查询能力，商户通过商户订单号主动查询协议状态及详情，完成下一步业务逻辑。

适用场景：
1. 商户后台、网络、服务器等出现异常，商户系统最终未接收到协议结果通知。
2. 商户需要查询用户签订的协议号。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/protocol/getProtocol
- 生产URL: https://api.payby.com/sgs/api/protocol/getProtocol
- 提交方式: POST
- 传输方式: HTTPS
- 数据格式: JSON
- 字符编码: UTF-8
- 签名算法: SHA256WithRSA

## 入参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | Sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

### Http Body
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581450087000 | |
| 业务内容 | bizContent | Required | GetProtocolRequest | - | 业务内容 |

### GetProtocolRequest
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | Me23484 | 仅支持字母、数字、中划线-、下划线_的组合，须保持唯一性 |

## 出参
### Http Header
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 签名 | sign | Required | String |

### Http Body
body 字段仅在 applyStatus=SUCCESS 且 code=0 时才返回。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | GetProtocolResponse |

### ResponseHeader
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求状态 | applyStatus | Required | String(16) | SUCCESS / FAIL / ERROR |
| 返回错误码 | code | Required | String(10) | 返回码 |
| 返回信息 | msg | Optional | String(200) | 返回信息 |

### GetProtocolResponse
| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 协议信息 | protocol | Required | Protocol |

### Protocol
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | |
| PayBy协议号 | authProtocolNo | Optional | String(32) | |
| 申请签约状态 | applySignStatus | Required | String(32) | APPLYING / CLOSED / SIGNED / FAILURE |
| 签约时间 | signTime | Optional | Timestamp(3) | |
| 生效时间 | effectTime | Optional | Timestamp(3) | |
| 失效时间 | invalidTime | Optional | Timestamp(3) | |
| 协议状态 | protocolStatus | Optional | String(32) | EXPIRED / TERMINATED / EFFECTIVE / INEFFECTIVE |
| 签约人ID | signerId | Optional | String(32) | 签约人在PayBy的会员ID |
| 扣除类型 | deductType | Optional | String(32) | SP=Single Pay Method |
| 扩展信息 | extension | Optional | Map<String,String> | payMethodType(BALANCE/CARD_PAY)、lastFour、cardBrand(VISA/MASTERCARD/CUP/JCB/DINERS/MAESTRO/AE/EBT/DISCOVER/CIRRUS/RUPAY/UATP/ELO) |

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
- 请求必须 HTTPS+POST+JSON+UTF-8，Header 必带 Sign、Partner-Id；签名使用 SHA256WithRSA 对 Http Body 原文签名，结果 Base64。
- merchantOrderNo 为 Required，缺失或格式非法应返回 400 INVALID_PARAMETER。
- merchantOrderNo 不存在的订单返回 90005 MERCHANT_ORDER_NO_NOT_EXIST。
- requestTime 偏离过大时分别返回 400 REQUESTTIME_TOO_EARLY / REQUESTTIME_TOO_LATER。
- 频率超限返回 402 RATE_LIMIT_REJECT；未授权返回 403；服务不可用返回 404；系统异常 500；超时 504；风控失败 601。
- 仅当 applyStatus=SUCCESS 且 code=0 时响应 body 才返回 protocol，对其他场景应校验 body 不返回。
- 校验 applySignStatus 枚举值范围：APPLYING/CLOSED/SIGNED/FAILURE；protocolStatus 枚举值范围：EXP
