---
title: PayBy收单交易数据模型
domain: acquire-transaction
kind: wiki_page
slug: payby-acquire-data-models
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:1d3b3713-3d92-4fd2-a760-42f5f4e3a4b6
tags: []
---

# PayBy收单交易数据模型

本页定义 PayBy 收单交易接口中使用到的核心数据结构与字段，包括订单主体 `AcquireOrder`、支付信息 `PaymentInfo`、卡片信息 `CardInfo` 以及金额、附属内容、商品明细等子对象。字段命名、类型、长度、枚举值原样保留，便于商户系统对接时直接映射。

相关说明参见 [[payby-acquire-protocol-rules]]、[[payby-acquire-payscene-params]]、[[payby-acquire-transaction-overview]]。

## AcquireOrder（收单订单）

收单订单的完整结构，作为创建订单返回与查询订单返回的主要载体。

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | - |
| 商户订单号 | merchantOrderNo | Required | String(64) | - |
| PayBy订单号 | orderNo | Required | String(32) | - |
| 订单状态 | status | Required | AcquireOrderStatus | - |
| 支付信息 | paymentInfo | Optional | PaymentInfo | - |
| 产品名称 | product | Required | String(200) | 例：Basic Payment Gateway |
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
| 冲正标志 | revoked | Required | String(32) | 为 true 时判定订单冲正成功 |
| 保留字段 | reserved | Optional | String(20) | - |
| 分账信息列表 | sharingInfoList | Optional | List<SharingInfo> | - |
| 优惠券列表 | promotionInfoList | Optional | List<PromotionInfo> | - |
| 商品标题阿语 | subjectAr | Optional | String(200) | - |

> 商户订单号 `merchantOrderNo` 仅支持字母、数字、中划线 `-`、下划线 `_`，需保持唯一；已支付或已取消的订单号不可复用。

## PaymentInfo（支付信息）

订单支付完成后的支付明细。

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 支付金额 | paidAmount | Required | Money | - |
| 支付时间 | paidTime | Required | Timestamp(3) | - |
| 付款人会员号 | payerMid | Optional | String(200) | - |
| 付款人手续费 | payerFeeAmount | Optional | Money | - |
| 收款人手续费 | payeeFeeAmount | Optional | Money | - |
| 支付渠道 | payChannel | Required | String(32) | BALANCE-余额 |
| 结算金额 | settlementAmount | Optional | Money | - |
| 卡信息 | cardInfo | Optional | CardInfo | - |
| 渠道参数 | channelParam | Optional | ChannelParam | - |

### ChannelParam（渠道参数）

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| eciValue | eciValue | Optional | String(32) |

## CardInfo（卡信息）

DIRECTPAY 等场景下返回的银行卡信息。

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 发卡组织 | brand | Required | String(32) | MASTERCARD / VISA / AE / DISCOVER / JCB |
| 卡号后4位 | last4 | Required | String(32) | - |
| 卡类型 | cardType | Required | String(32) | DC-借记卡 CC-贷记卡 |
| 失效月份 | expMonth | Optional | String(32) | - |
| 失效年份 | expYear | Optional | String(32) | - |
| cardToken | cardToken | Optional | String(32) | 用于 savedCard 支付 |
| cardToken过期时间 | cardTokenExpTime | Optional | Timestamp(3) | Card token expiration time |
| 发卡国 | issueCountry | Optional | String(32) | - |
| 发卡行 | issueBank | Optional | String(32) | - |

## Money（金额）

| 字段名 | 变量名 | 必填 | 类型 | 示例 |
| --- | --- | --- | --- | --- |
| 金额 | amount | Required | Decimal(12,2) | 123.45 |
| 币种 | currency | Required | String(32) | AED |

## AccessoryContent（附属内容）

订单可携带的附加结构化信息，用于金额拆解、商品与终端补充。

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 金额明细 | amountDetail | Optional | AmountDetail |
| 商品明细 | goodsDetail | Optional | GoodsDetail |
| 终端明细 | terminalDetail | Optional | TerminalDetail |

### AmountDetail（金额明细）

| 字段名 | 变量名 | 必填 | 类型 |
| --- | --- | --- | --- |
| 折扣金额 | discountableAmount | Optional | Money |
| 净值金额 | amount | Optional | Money |
| 附加税金额 | vatAmount | Optional | Money |
| 消费金额 | tipAmount | Optional | Money |

### GoodsDetail（商品明细）

| 字段名 | 变量名 | 必填 | 类型 | 示例 |
| --- | --- | --- | --- | --- |
| 商品描述 | body | Optional | String(64) | Apple Gifts |
| 商品类目树 | categoriesTree | Optional | String(64) | - |
| 商品类目 | goodsCategory | Optional | String(64) | - |
| 商品编号 | goodsId | Optional | String | - |

> 原文中 `GoodsDetail` 表格在文末截断，已收录可见字段。`TerminalDetail` 详细字段未在原文片段中给出。

## 关联结构提示

- `AcquireOrderStatus`、`SharingInfo`、`PromotionInfo` 等枚举/子结构属订单状态与分账/优惠券域，详见对应章节。
- 字段如何按支付场景填充（如 DIRECTPAY 返回 `cardInfo`、JSAPI 返回 `
