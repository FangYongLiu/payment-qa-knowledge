---
id: api_payby_place_transfer_to_bank_order
object_type: API
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p14
tags:
- transfer
- payout
- bank
subdomain: transfer-to-bank
module: null
sensitivity: normal
name: 创建单笔付款到银行卡订单
aliases:
- placeTransferToBankOrder
related_services:
- svc_transfer
---

## 用途
商户将账户中的资金付款到指定的收款银行账户(IBAN)。订单状态机：CREATED / SUCCESS / FAILURE / BANK_FAIL。

## 路径/方法
- 联调URL: `https://uat.test2pay.com/sgs/api/transfer/placeTransferToBankOrder`
- 生产URL: `https://api.payby.com/sgs/api/transfer/placeTransferToBankOrder`
- 方法: HTTP POST，Content-Type: application/json

## 入参
### Http Header
| 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|
| Content-Language | Optional | String(10) | en-英文 |
| sign | Required | String | 签名 |
| Partner-Id | Required | String(12) | 商户号 |

### Http Body
| 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|
| requestTime | Required | Timestamp(3) | 请求时间 |
| bizContent | Required | PlaceTransferToBankOrderRequest | 业务内容 |

### PlaceTransferToBankOrderRequest
| 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|
| merchantOrderNo | Required | String(64) | 商户订单号 |
| holderName | Required | String(100) | 收款人姓名(加密传输) |
| iban | Required | String(34) | 收款人IBAN(加密传输) |
| swiftCode | Optional | String(11) | 收款银行SwiftCode，填写正确可提升正确率 |
| beneficiaryAddress | Optional | String(100) | 收款人地址(加密传输)。若收款账户为个人账户，必须传入；holderName + beneficiaryAddress 字符总长不得超过 140，否则可能转账失败 |
| amount | Required | Money | 企业付款金额(amount + currency，例如 AED) |
| memo | Required | String(128) | 付款备注 |
| notifyUrl | Optional | String(200) | 后端通知地址 |

加密字段：holderName、iban、beneficiaryAddress。

## 出参
### Http Header
| 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|
| Content-Language | Optional | String(10) | en-英文 |
| Sign | Required | String | 签名 |
| Partner-Id | Required | String(12) | 商户号 |

### Http Body
| 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|
| head | Required | ResponseHeader | 响应头(applyStatus/code/msg/traceCode) |
| body | Optional | PlaceTransferToBankOrderResponse | 响应体 |

### PlaceTransferToBankOrderResponse
| 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|
| transferToBankOrder | Required | TransferToBankOrder | 订单信息 |

TransferToBankOrder 主要字段(响应样例)：amount、holderName(密文)、iban(密文)、beneficiaryAddress(密文)、memo、merchantOrderNo、notifyUrl、orderNo、product("Transfer To Bank")、requestTime、status(如 CREATED)、swiftCode。

## 错误码
| code | msg | 原因 | 解决方案 |
|---|---|---|---|
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy,稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |
| 62002 | ORDER_FAILURE | 订单已失败 | 调整商户订单号 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同但业务参数不同的创建请求 | 调整订单号 |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 | 请申请产品 |
| 62028 | ORDER_SUCCESS | 订单已成功 | 调整商户订单号 |
| 62029 | ORDER_CREATED | 订单已创建 | 调整商户订单号 |

## 测试校验点
- Header 校验：Partner-Id、sign 必填；Content-Language 可选(en)。
- 必填参数校验：requestTime、bizContent.merchantOrderNo、holderName、iban、amount、memo 缺失返回 400 INVALID_PARAMETER。
- 字段长度边界：merchantOrderNo(64)、holderName(100)、iban(34)、swiftCode(11)、beneficiaryAddress(100)、memo(128)、notifyUrl(200)。
- 加密字段：holderName、iban、beneficiaryAddress 必须按约定加密传输；响应中这些字段返回密文(响应样例为 hex 字符串)。
- 个人收款账户场景：必须传 beneficiaryAddress，且 holderName+beneficiaryAddress 字符总和 ≤ 140，否则可能转账失败。
- requestTime 时间窗口：过早返回 REQUESTTIME_TOO_EARLY，过晚返回 REQUESTTIME_TOO_LATER。
- 幂等/重复提交：相同 merchantOrderNo + 相同业务参数 → 命中 ORDER_CREATED(62029)/ORDER_SUCCESS(62028)/ORDER_FAILURE(62002)；相同订单号但参数不同 → MERCHANT_ORDER_NO_EXIST(62016)。
- 限流：高频调用应触发 RATE_LIMIT_REJECT(402)。
- 鉴权与产品权限：未授权返回 UNAUTHORIZED(403)；未申请产品返回 PRODUCT_IS_NOT_APPLIED(62026)。
- 风控校验：触发风控返回 RISK_FAIL(601)。
- 金额 amount：currency=AED 等合法币种，金额小数位与 Money 类型一致(示
