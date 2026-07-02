---
id: api_transfer_place_to_bank_order
object_type: API
domain: wallet
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p2
tags:
- transfer
- payout
- bank
subdomain: null
module: null
sensitivity: normal
name: 单笔付款到银行卡下单接口
aliases:
- placeTransferToBankOrder
related_services:
- svc_transfer
---

## 用途
商户将账户资金付款到指定的收款银行账户，创建单笔付款到银行卡订单（placeTransferToBankOrder）。

订单状态机：
- CREATED 已创建
- SUCCESS 已成功
- FAILURE 已失败
- BANK_FAIL 银行退票

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/transfer/placeTransferToBankOrder
- 生产URL: https://api.payby.com/sgs/api/transfer/placeTransferToBankOrder
- 方法：HTTP POST，Content-Type: application/json

## 入参
Http Header

| 字段 | 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|---|
| 文案语言 | Content-Language | Optional | String(10) | en-英文 |
| 签名 | sign | Required | String | |
| 商户号 | Partner-Id | Required | String(12) | |

Http Body

| 字段 | 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|---|
| 请求时间 | requestTime | Required | Timestamp(3) | |
| 业务内容 | bizContent | Required | PlaceTransferToBankOrderRequest | |

PlaceTransferToBankOrderRequest

| 字段 | 变量名 | 必填 | 类型 | 描述 |
|---|---|---|---|---|
| 商户订单号 | merchantOrderNo | Required | String(64) | |
| 受益人姓名 | holderName | Required | String(100) | 加密传输 |
| IBAN | iban | Optional | String(34) | 加密传输 |
| SWIFT Code | swiftCode | Optional | String(11) | 填写正确可提升正确率 |
| 收款人地址 | beneficiaryAddress | Optional | String(140) | 加密传输；个人账户必传，且 holderName + beneficiaryAddress 字符总和不超过 140 |
| 金额 | amount | Required | Money | 企业付款金额 |
| 付款备注 | memo | Required | String(128) | |
| 后端通知地址 | notifyUrl | Optional | String(200) | |
| 账户号 | accountNo | Optional | String(64) | 加密传输（since v2.1） |
| 网络代码 | networkCode | Optional | String(16) | 默认 LOCAL（since v2.1） |
| 银行名称 | bankName | Optional | String(50) | |
| 国家代码 | countryCode | Optional | String(16) | 默认 AE（since v2.1） |
| 城市代码 | cityCode | Optional | String(16) | since v2.3 |
| 到账币种 | fundoutCurrencyCode | Optional | String(16) | 默认 AED（since v2.1） |
| Fed wire | fedwireCode | Optional | String(9) | since v2.1 |
| 分支行名称 | branchName | Optional | String(35) | |
| 中间行 | intermediaryBank | Optional | String(11) | since v2.1 |
| 受益人类型 | beneficiaryType | Optional | String(16) | 默认 IBAN（since v2.1） |
| purposeCode | purposeCode | Optional | String(16) | |

受益人类型字段关联（IBAN/BBAN/FED_WIRE）：

| 字段 | IBAN | BBAN | FED_WIRE |
|---|---|---|---|
| holderName | Required | Required | Required |
| iban | Required | Forbidden | Forbidden |
| swiftCode | Optional | Required | Forbidden |
| beneficiaryAddress | Required | Required | Required |
| accountNo | Forbidden | Required | Required |
| bankName | Optional | Optional | Optional |
| fedwireCode | Forbidden | Forbidden | Required |
| branchName | Optional | Optional | Optional |
| intermediaryBank | Optional | Optional | Optional |

## 出参
Http Header：Content-Language(Optional)、Sign(Required)、Partner-Id(Required)

Http Body

| 字段 | 变量名 | 必填 | 类型 |
|---|---|---|---|
| 响应头 | head | Required | ResponseHeader |
| 响应体 | body | Optional | PlaceTransferToBankOrderResponse |

PlaceTransferToBankOrderResponse

| 字段 | 变量名 | 必填 | 类型 |
|---|---|---|---|
| 订单信息 | transferToBankOrder | Required | TransferToBankOrder |

响应样例中 TransferToBankOrder 包含：merchantOrderNo、orderNo、status、holderName、iban、swiftCode、amount、notifyUrl、memo、requestTime、product、paymentInfo（payerFeeAmount、arrivalTime）、beneficiaryAddress、networkCode。

## 错误码

| code | msg | 原因 | 解决方案 |
|---|---|---|---|
| 0 | SUCCESS | 成功 | |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间太早 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间太晚 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |
| 62002 | ORDER_FAILURE | 订单已失败 | 调整商户订单号 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同但参数不同的重复创建 | 调整订单号 |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 | 请申请产品 |
| 62028 | ORDER_SUCCESS | 订单已成功 | 调整商户订单号 |
| 62029 | ORDER_CREATED | 订单已创建 | 调整商户订单号 |
| 62094 | THE_ENTERED_COUNTRY_CODE_IS_INVALID | 国家码校验失败 | 调整请求参数 |
| 62095 | THE_ENTERED_CITY_CODE_IS_INVALID | 城市码校验失败 | 调整请求
