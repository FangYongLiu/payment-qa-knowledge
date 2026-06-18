---
id: api_acquire_place_order
object_type: API
domain: payby-acquire-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p9
tags:
- 收单
- 预支付
- 幂等
subdomain: null
module: null
sensitivity: normal
name: 创建订单接口(placeOrder)
aliases:
- placeOrder
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
商户系统先调用该接口在PayBy服务后台生成预支付订单，返回正确的Token订单会话标识后再调起支付。该接口为幂等接口，相同请求重复请求多次将返回当前订单状态；幂等请求不校验请求时间，多次请求时订单请求时间以第一次请求为准。

订单状态机 AcquireOrderStatus：
- CREATED 已创建
- PAID_SUCCESS 支付成功
- SETTLED 结算成功
- FAILURE 订单失败
- AUTHORIZATION 预授权成功
- VOID 预授权取消成功

## 路径/方法
- 联调URL: https://uat.test2pay.com/sgs/api/acquire2/placeOrder
- 生产URL: https://api.payby.com/sgs/api/acquire2/placeOrder
- 方法: HTTP POST (JSON)

## 入参
Http Header
- Content-Language Optional String(10) 文案语言，en-英文(默认)
- sign Required String 签名
- Partner-Id Required String(12) 商户号

Http Body
- requestTime Required Timestamp(3) 请求时间
- bizContent Required PlaceAcquireOrderRequest 业务内容

PlaceAcquireOrderRequest
- merchantOrderNo Required String(64) 商户订单号
- subject Required String(64) 商品标题
- totalAmount Required Money 订单金额
- expiredTime Optional Timestamp(3) 过期时间，不得超过请求时间48小时，默认2小时
- payeeMid Optional String(20) 收款人会员号，不填默认是商户自己
- paySceneCode Required String(200) 支付场景码
- paySceneParams Optional String(512) 支付场景参数
- notifyUrl Optional String(200) 后端通知地址
- deviceId Optional String(200) 终端ID，二级商户号有值时必填
- secondaryMerchantId Optional String(64) 二级商户号
- accessoryContent Optional AccessoryContent 附属内容
- reserved Optional String(20) 保留字段
- sharingParamList Optional List<SharingParam> 分账参数列表，订单退款时退款金额从payeeMid账户扣减
- promotionInfoList Optional List<PromotionInfo> 优惠券列表
- subjectAr Optional String(200) 商品标题阿语

SharingParam
- sharingAmount Required Money 金额
- sharingIdentity Required String(200) 分账方标识 (PHONE_NO 时为带区号的手机号；MEMBER_ID 时为 PayBy member ID；请求需加密)
- sharingIdentitySeqId Required Integer 序号(不能重复，从1开始连号)
- sharingMemo Required String(128) 备注
- sharingIdentityType Required String(64) 分账方标识类型 PHONE_NO / MEMBER_ID / TOTOK_UID
- withholdAndRemitFee Optional Boolean 分账方代收代缴支付手续费，所有分账条目中最多出现一次或不出现，不出现则默认无手续费策略

PromotionInfo
- appliedRewardId Required String(64) 优惠券ID
- settleFlag Required String(32) 结算标识 YES / NO

## 出参
Http Header
- sign Required String 签名

Http Body
- head Required ResponseHeader 响应头
- body Optional PlaceOrderResponse 响应体（仅在 applyStatus=SUCCESS 且 code=0 时才返回）

PlaceAcquireOrderResponse
- acquireOrder Optional AcquireOrder 订单信息
- interactionParams Optional InteractionParams 支付参数

仅在订单状态是 CREATED 时，将根据不同的 paySceneCode 返回不同的 interactionParams。

## 错误码
| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | - |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API未授权 | 联系PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API服务不可用 | 联系PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系PayBy/稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 调整业务 |
| 62001 | ORDER_PAID | 订单已支付成功不支持撤销 | 调整商户订单号 |
| 62002 | ORDER_FAILURE | 已失败的订单发起创建订单 | 调整商户订单号 |
| 62003 | ORDER_SETTLED | 已结算的订单发起创建订单 | 调整商户订单号 |
| 62008 | EXPIREDTIME_LESS_THAN_REQUESTTIME | 过期时间小于请求时间 | 调整过期时间 |
| 62009 | EXPIREDTIME_TOO_LATER | 过期时间超过请求时间48小时 | 调整过期时间 |
| 62012 | PAYSCENECODE_ILLEGAL | 支付场景码非法 | 调整支付场景码 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同,不同业务参数的重复创建订单请求 | 调整订单号 |
| 62018 | PAYERMID_NOT_EXIST | 付款方账号填写错误 | 调整付款方账号 |
| 62019 | PAYEEMID_NOT_EXIST | 收款方账号填写错误 | 调整收款方账户 |
| 62020 | PAYERMID_PAYEEMID_ARE_SAME | 付款方和收款方账号一样 | 调整付款方或者收款方账号 |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 | 请申请产品 |
| 62031 | MISSING_IAP_DEVICE_ID | 缺少iapDeviceId | 调整请求参数 |
| 62032 | MISSING_APP_ID | 缺少AppId | 调整请求参数 |
| 62033 | MISSING_AUTHCODE | 缺少authCode | 调整请求参数 |
| 62034 | INVALID_APP_ID | 无效的appId | 调整请求参数 |
| 62036 |
