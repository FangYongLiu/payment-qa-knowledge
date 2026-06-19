---
title: PayBy API 订单数据结构定义
domain: merchant-portal
kind: wiki_page
slug: payby-api-order-data-structures
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p6
tags: []
---

# PayBy API 订单数据结构定义

本页汇总 PayBy 接口中订单相关对象的字段定义，覆盖收单、退款、转账、银行转账等业务对象，以及它们引用的支付信息、卡信息、金额/商品/终端明细等附属结构。所有字段名、类型、枚举值与原文保持一致。

## 商户订单号约定

- 仅支持字母、数字、`-`、`_` 的英文半角字符组合，由商户自定义生成。
- 必须保持唯一性（建议系统时间 + 随机序列）。
- 重新发起一笔支付要使用原订单号，避免重复支付。
- 已支付或已取消的订单号不能重新发起支付。

## AcquireOrder（收单订单）

收单订单主对象，包含订单基础信息、状态、金额、支付场景、附属内容、分账与优惠信息等。

| 字段 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) |
| 商户订单号 | merchantOrderNo | Required | String(64) |
| PayBy 订单号 | orderNo | Required | String(32) |
| 订单状态 | status | Required | AcquireOrderStatus |
| 支付信息 | paymentInfo | Optional | PaymentInfo |
| 产品名称 | product | Required | String(200) |
| 订单金额 | totalAmount | Required | Money |
| 收款方会员号 | payeeMid | Required | String(200) |
| 过期时间 | expiredTime | Required | Timestamp(3) |
| 后台通知地址 | notifyUrl | Required | String(200) |
| 商品标题 | subject | Required | String(200) |
| 附属内容 | accessoryContent | Optional | AccessoryContent |
| 支付场景代码 | paySceneCode | Required | String(200) |
| 支付场景参数 | paySceneParams | Required | String(512) |
| 终端ID | deviceId | Optional | String(200) |
| 二级商户号 | secondaryMerchantId | Optional | String(64) |
| 错误代码 | failCode | Optional | String(50) |
| 错误描述 | failDes | Optional | String(200) |
| 冲正标志 | revoked | Required | String(32) |
| 保留字段 | reserved | Optional | String(20) |
| 分账信息列表 | sharingInfoList | Optional | List\<SharingInfo\> |
| 优惠券列表 | promotionInfoList | Optional | List\<PromotionInfo\> |
| 商品标题阿语 | subjectAr | Optional | String(200) |
| 账号充值交易参数 | accountFundingParameter | Optional | AccountFundingParameter |
| PayFacs 子商户信息 | payFacsSubMerchant | Optional | PayFacsSubMerchant |

要点：

- `revoked` 为 `true` 时判定该订单冲正成功。
- `accountFundingParameter`：开通 AFT 交易权限，且 `paySceneCode` 为 `PAYPAGE`、`INAPP`、`AUTODEBIT`、`DIRECTPAY`、`PAYANDSIGN` 时必传，其他情况为 null。
- `payFacsSubMerchant`：PayFacs 交易使用，需商户开通权限。
- `failCode` / `failDes`：订单失败原因代码与描述。

## PaymentInfo（支付信息）

| 字段 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 支付金额 | paidAmount | Required | Money |
| 支付时间 | paidTime | Required | Timestamp(3) |
| 付款人会员号 | payerMid | Optional | String(200) |
| 付款人手续费 | payerFeeAmount | Optional | Money |
| 收款人手续费 | payeeFeeAmount | Optional | Money |
| 支付渠道 | payChannel | Required | String(32) |
| 结算金额 | settlementAmount | Optional | Money |
| 卡信息 | cardInfo | Optional | CardInfo |
| 渠道参数 | channelParam | Optional | ChannelParam |

- `payChannel`：例如 `BALANCE-余额`。

### ChannelParam（渠道参数）

| 字段 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| eciValue | eciValue | Optional | String(32) |
| extension | extension | Optional | String(1024) |

`extension` 以 JSON 格式返回 `AuthCode`、`RRN`、`Stan`、`AcquireCode`、`AcquireMessage` 等字段，例如：

```json
{"AuthCode":"245408","Stan":"245408","AcquireCode":"00","AcquireMessage":"Approved","RRN":"529512245408"}
```

### CardInfo（卡信息）

| 字段 | 变量名 | 必填 | 类型 | 说明 |
| --- | --- | --- | --- | --- |
| 发卡组织 | brand | Required | String(32) | MASTERCARD / VISA / AE / DISCOVER / JCB |
| 卡号后 4 位 | last4 | Required | String(32) | |
| 卡类型 | cardType | Required | String(32) | DC-借记卡，CC-贷记卡 |
| 失效月份 | expMonth | Optional | String(32) | |
| 失效年份 | expYear | Optional | String(32) | |
| cardToken | cardToken | Optional | String(32) | |
| cardToken 过期时间 | cardTokenExpTime | Optional | Timestamp(3) | |
| 发卡国 | issueCountry | Optional | String(32) | |
| 发卡行 | issueBank | Optional | String(32) | |

## Money（金额）

| 字段 | 变量名 | 必填 | 类型 | 示例 |
| --- | --- | --- | --- | --- |
| 金额 | amount | Required | Decimal(12,2) | 123.45 |
| 币种 | currency | Required | String(32) | AED |

## AccessoryContent（附属内容）

承载订单附属的金额、商品、终端等明细。

| 字段 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 金额明细 | amountDetail | Optional | AmountDetail |
| 商品明细 | goodsDetail | Optional | GoodsDetail |
| 终端明细 | terminalDetail | Optional | TerminalDetail |

### AmountDetail（金额明细）

| 字段 | 变量名 | 类型 |
| --- | --- | --- |
| 折扣金额 | discountableAmount | Money |
| 净值金额 | amount | Money |
| 附加税金额 | vatAmount | Money |
| 消费金额 | tipAmount | Money |

字段均为 Optional。

### GoodsDetail（商品明细）

| 字段 | 变量名 | 类型 |
| --- | --- | --- |
| 商品描述 | body | String(64) |
| 商品类目树 | categoriesTree | String(64) |
| 商品类目 | goodsCategory | String(64) |
| 商品编号 | goodsId | String(200) |
| 商品名称 | goodsName | String(64) |
|
