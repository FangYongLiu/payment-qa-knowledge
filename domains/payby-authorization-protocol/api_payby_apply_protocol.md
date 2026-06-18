---
id: api_payby_apply_protocol
object_type: API
domain: payby-authorization-protocol
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-auth-agreement-v1.0.2-p1
tags:
- POST
- HTTPS
- JSON
- SHA256WithRSA
subdomain: null
module: null
sensitivity: normal
name: 申请签约协议
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
用于发起商户会员 & 商户 & PayBy 三方签约协议。调用成功后返回 tokenUrl，商户系统可使用 token 或完整 URL 呼起 PayBy 完成支付。tokenUrl 有效期为 1 小时，超过有效期需使用相同业务内容参数重新发起以获取新的 tokenUrl。

## 路径/方法
- 方法: POST
- 传输方式: HTTPS
- 数据格式: JSON
- 字符编码: UTF-8
- 联调URL: https://uat.test2pay.com/sgs/api/protocol/applyProtocol
- 生产URL: https://api.payby.com/sgs/api/protocol/applyProtocol

## 入参
### Http Header
| 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- |
| Content-Language | Optional | String(10) | en-英文 |
| Sign | Required | String | 签名(SHA256WithRSA, Base64) |
| Partner-Id | Required | String(12) | 商户号 |

### Http Body
| 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- |
| requestTime | Required | Timestamp(3) | 请求时间 |
| bizContent | Required | ApplyProtocolRequest | 业务内容 |

### ApplyProtocolRequest
| 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- |
| merchantOrderNo | Required | String(64) | 商户订单号，仅支持字母、数字、`-`、`_`，需保持唯一；已支付或已取消的不能复用 |
| notifyUrl | Optional | String(200) | 商户接收通知的地址 |
| langType | Optional | String(32) | en-英文 / zh-中文 / ar-阿语 |
| signerMerchantId | Required | String(200) | 签约人商户端 id，加密传输(RSA 公钥加密 + Base64) |
| protocolSceneCode | Required | String(32) | 协议场景码，目前 110=付款授权 |
| expiredTime | Optional | Timestamp(3) | 过期时间，默认 15 分钟 |
| protocolSceneParams | Required | String(512) | 协议场景需要的参数 |
| accessType | Optional | String(32) | SDK / H5，参数为空默认 SDK |

### 协议场景参数关系
| accessType | protocolSceneCode | protocolSceneParams |
| --- | --- | --- |
| SDK | 110 | iapDeviceId(必填)、appId(必填) |
| H5  | 110 | redirectUrl(可空) |

## 出参
### Http Header
| 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- |
| Content-Language | Optional | String(10) | en-英文 |
| Sign | Required | String | 签名 |
| Partner-Id | Required | String(12) | 商户号 |

### Http Body
| 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- |
| head | Required | ResponseHeader | 响应头 |
| body | Optional | ApplyProtocolResponse | 响应体；仅在 applyStatus=SUCCESS 且 code=0 时返回 |

### ResponseHeader
| 变量名 | 类型 | 描述 |
| --- | --- | --- |
| applyStatus | String(16) | SUCCESS / FAIL / ERROR |
| code | String(10) | 返回码 |
| msg | String(200) | 返回信息 |

### ApplyProtocolResponse
| 变量名 | 必填 | 类型 |
| --- | --- | --- |
| interActionParams | Optional | InterActionParams |

### InterActionParams
| 变量名 | 类型 | 描述 |
| --- | --- | --- |
| tokenUrl | String(200) | 包含 Token 的 URL，商户可用 token 或完整 URL 呼起 PayBy 完成支付，有效期 1 小时 |

## 错误码
| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API 未授权 | 联系 ToPay |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 | 联系 ToPay |
| 500 | SYSTEM_ERROR | 系统错误 | 联系 ToPay，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |
| 90001 | MISSING_IAP_DEVICE_ID | 缺少 deviceId | 调整请求参数 |
| 90002 | MISSING_APP_ID | 缺少 appId | 调整请求参数 |
| 90003 | INVALID_APP_ID | 无效的 appId | 调整请求参数 |
| 90004 | INVALID_LANG_TYPE | 无效的语言类型 | 调整请求参数 |
| 90006 | INVALID_PROTOCOL_SCENE_CODE | 无效的 protocolSceneCode | 调整场景代码 |
| 90007 | EXPIREDTIME_ILLEGAL | 过期时间非法 | 调整过期时间 |
| 90008 | EXPIREDTIME_LESS_THAN_REQUESTTIME | 过期时间小于请求时间 | 调整过期时间 |
| 90009 | INVALID_ACCESS_TYPE | 无效的 accessType | 调整请求参数 |

## 测试校验点
- 协议必须为 HTTPS + POST + JSON + UTF-8；签名算法 SHA256WithRSA，原文为请求 Http Body 原始内容，签名结果 Base64。
- Header 三件套：Content-Language(可选 en)、Sign(必填)、Partner-Id(必填，String(12))。
- requestTime/bizContent 必填；requestTime 偏离当前过早或过晚分别命中 400 REQUESTTIME_TOO_EARLY/REQUESTTIME_TOO_LATER。
- merchantOrderNo 仅支持字母/数字/`-`/`_`；唯一；已支付
