---
id: api_payby_apply_protocol
object_type: API
domain: payby-authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: upload:c28e6aeb-4485-4713-83f7-c926b25d5235
tags:
- 签约
- 协议
- POST
- HTTPS
subdomain: null
module: null
sensitivity: normal
name: 申请签约协议接口
aliases:
- applyProtocol
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用于发起商户会员、商户与PayBy三方签约协议申请，返回 tokenUrl 用于呼起支付。tokenUrl 有效期为1小时，超时后需使用相同业务内容重新发起申请获取新的 tokenUrl。

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/protocol/applyProtocol
- 生产URL: https://api.payby.com/sgs/api/protocol/applyProtocol
- 提交方式: POST
- 传输方式: HTTPS
- 数据格式: JSON
- 字符编码: UTF-8
- 签名算法: SHA256WithRSA（请求和响应均需签名）

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
| 业务内容 | bizContent | Required | ApplyProtocolRequest | - | 业务内容 |

### ApplyProtocolRequest
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | Me23484 | |
| 后端通知地址 | notifyUrl | Optional | String(200) | - | 商户接收通知的地址 |
| 协议文案语言 | langType | Optional | String(32) | en | en-英文 / zh-中文 / ar-阿语 |
| 签约人标识 | signerMerchantId | Required | String(200) | 158149389 | 签约人商户端id，加密传输 |
| 协议场景码 | protocolSceneCode | Required | String(32) | 110 | 110=付款授权 |
| 过期时间 | expiredTime | Optional | Timestamp(3) | 1581493898000 | 默认15分钟 |
| 协议场景参数 | protocolSceneParams | Required | String(512) | | 协议场景需要的参数 |
| 访问类型 | accessType | Optional | String(32) | SDK | SDK / H5；为空默认SDK |

### 协议场景参数关系
| accessType | protocolSceneCode | protocolSceneParams | interActionParams |
| --- | --- | --- | --- |
| SDK | 110 | iapDeviceId(必填)、appId(必填) | tokenUrl |
| H5 | 110 | redirectUrl(可空) | tokenUrl |

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
| 响应体 | body | Optional | ApplyProtocolResponse | applyStatus=SUCCESS 且 code=0 时才返回 |

### ResponseHeader
| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求状态 | applyStatus | Required | String(16) | SUCCESS | SUCCESS-申请成功 / FAIL-申请失败 / ERROR-申请异常 |
| 返回错误码 | code | Required | String(10) | 0 | 返回码 |
| 返回信息 | msg | Optional | String(200) | - | 返回信息 |

### ApplyProtocolResponse
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 交互参数 | interActionParams | Optional | InterActionParams | |

### InterActionParams
| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 令牌地址 | tokenUrl | Required | String(200) | URL地址，包含Token，可用于商户系统呼起PayBy完成支付，有效期1小时 |

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
| 90001 | MISSING_IAP_DEVICE_ID | 缺少deviceId | 调整请求参数 |
| 90002 | MISSING_APP_ID | 缺少appId | 调整请求参数 |
| 90003 | INVALID_APP_ID | 无效的appId | 调整请求参数 |
| 90004 | INVALID_LANG_TYPE | 无效的语言类型 | 调整请求参数 |
| 90006 | INVALID_PROTOCOL_SCENE_CODE | 无效的protocolSceneCode | 调整场景代码 |
| 90007 | EXPIREDTIME_ILLEGAL | 过期时间非法 | 调整过期时间 |
| 90008 | EXPIREDTIME_LESS_THAN_REQUESTTIME | 过期时间小于请求时间 | 调整过期时间 |
| 90009 | INVALID_ACCESS_TY
