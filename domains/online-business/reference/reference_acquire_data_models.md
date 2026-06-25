---
id: reference_acquire_data_models
object_type: Reference
name: 收单交易接口数据模型(AcquireOrder / PaymentInfo / CardInfo 等)
aliases: [AcquireOrder, PaymentInfo, CardInfo, SharingParam, AcquireOrderStatus]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki_attachment
source_ref: wiki_attachment:1d3b3713 (PayBy 收单交易数据模型)
tags: [online-business, acquiring, data-model, AcquireOrder]
related_services: [svc_acquireii, svc_sgs]
---

# 收单交易接口数据模型

> PayBy 收单接口的核心数据结构与字段(下单/查单/退款的共用载体)。字段名/类型/长度/枚举原样保留,QA 对接、断言、造数据的字段字典。

## AcquireOrder(收单订单,下单与查单返回主体)

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | - |
| 商户订单号 | merchantOrderNo | Required | String(64) | 唯一,字母/数字/-/_,不可复用 |
| PayBy订单号 | orderNo | Required | String(32) | - |
| 订单状态 | status | Required | AcquireOrderStatus | 见下状态机 |
| 支付信息 | paymentInfo | Optional | PaymentInfo | - |
| 产品名称 | product | Required | String(200) | 例 Basic Payment Gateway |
| 订单金额 | totalAmount | Required | Money | - |
| 收款方会员号 | payeeMid | Required | String(200) | - |
| 过期时间 | expiredTime | Required | Timestamp(3) | - |
| 后台通知地址 | notifyUrl | Required | String(200) | - |
| 商品标题 | subject | Required | String(200) | - |
| 附属内容 | accessoryContent | Optional | AccessoryContent | - |
| 支付场景代码 | paySceneCode | Required | String(200) | - |
| 支付场景参数 | paySceneParams | Required | String(512) | - |
| 终端ID | deviceId | Optional | String(200) | - |
| 二级商户号 | secondaryMerchantId | Optional | String(64) | - |
| 错误代码 | failCode | Optional | String(50) | 订单失败原因代码 |
| 错误描述 | failDes | Optional | String(200) | 订单失败原因 |
| 冲正标志 | revoked | Required | String(32) | true 时判定订单冲正成功 |
| 保留字段 | reserved | Optional | String(20) | - |
| 分账信息列表 | sharingInfoList | Optional | List<SharingInfo> | - |
| 优惠券列表 | promotionInfoList | Optional | List<PromotionInfo> | - |
| 商品标题阿语 | subjectAr | Optional | String(200) | - |

### AcquireOrderStatus 状态机
| Status | 说明 |
| --- | --- |
| CREATED | 已创建 |
| PAID_SUCCESS | 支付成功 |
| SETTLED | 结算成功 |
| FAILURE | 订单失败 |
| AUTHORIZATION | 预授权成功 |
| VOID | 预授权取消成功 |

## PaymentInfo(支付信息,支付完成后明细)

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 支付金额 | paidAmount | Required | Money | - |
| 支付时间 | paidTime | Required | Timestamp(3) | - |
| 付款人会员号 | payerMid | Optional | String(200) | - |
| 付款人手续费 | payerFeeAmount | Optional | Money | - |
| 收款人手续费 | payeeFeeAmount | Optional | Money | - |
| 支付渠道 | payChannel | Required | String(32) | 如 BALANCE-余额 |
| 结算金额 | settlementAmount | Optional | Money | - |
| 卡信息 | cardInfo | Optional | CardInfo | - |
| 渠道参数 | channelParam | Optional | ChannelParam | `eciValue` 等 |

## CardInfo(卡信息,DIRECTPAY 等场景返回)

| 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- |
| brand | Required | String(32) | MASTERCARD / VISA / AE / DISCOVER / JCB |
| last4 | Required | String(32) | 卡号后 4 位 |
| cardType | Required | String(32) | DC-借记卡 / CC-贷记卡 |
| expMonth / expYear | Optional | String(32) | 失效月/年 |
| cardToken | Optional | String(32) | 用于 savedCard 支付 |
| cardTokenExpTime | Optional | Timestamp(3) | cardToken 过期时间 |
| issueCountry / issueBank | Optional | String(32) | 发卡国 / 发卡行 |

## SharingParam(分账参数,下单/退款共用)

| 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- |
| sharingAmount | Required | Money | 分账金额 |
| sharingIdentity | Required | String(200) | 分账方标识;PHONE_NO 带区号 / MEMBER_ID 传会员ID;**需加密** |
| sharingIdentitySeqId | Required | Integer | 序号,从 1 起连号,不可重复 |
| sharingMemo | Required | String(128) | 备注 |
| sharingIdentityType | Required | String(64) | PHONE_NO / MEMBER_ID / TOTOK_UID |
| withholdAndRemitFee | Optional | Boolean | 分账方代收代缴手续费;所有分账条目中最多出现一次 |

## Money / AccessoryContent / 子明细

- **Money**:`amount`(Decimal(12,2),如 123.45)、`currency`(String(32),如 AED)。
- **AccessoryContent**:`amountDetail` / `goodsDetail` / `terminalDetail`(均可选)。
  - **AmountDetail**:`discountableAmount`(折扣金额) / `amount`(净值金额) / `vatAmount`(附加税) / `tipAmount`(消费金额),均 Money。
  - **GoodsDetail**:`body`(商品描述,如 Apple Gifts) / `categoriesTree` / `goodsCategory` / `goodsId`。
  - **TerminalDetail**:字段「待补:原文片段未给出」。

## 关联关系
- **所属服务**:[[svc_acquireii]] 收单核心 / 接入网关 [[svc_sgs]](= `related_services`)。
- **落库表**:[[tbl_acquireii_t_acquire_order]](订单主表)、[[tbl_acquireii_t_payment_info]]、[[tbl_acquireii_t_card_info]]、[[tbl_acquireii_t_sharing_info]]、[[tbl_acquireii_t_promotion_info]](由各表 `related_services` 反指)。
- **接口契约**:见 [[api_sgs_acquire_place_order]]、[[api_sgs_acquire_get_order]] 等。
- **枚举与协议**:见 [[reference_acquire_protocol_and_codes]]。

## QA 关注点
- AcquireOrder 字段与 `t_acquire_order` 落库的一致性;`revoked` 与冲正判定。
- DIRECTPAY 返回 cardInfo;加密字段不应明文落库/回传。
- 分账 sharingIdentitySeqId 连号校验;Money 币种与原单一致。
