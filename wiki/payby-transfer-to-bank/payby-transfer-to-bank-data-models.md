---
title: PayBy 转账到银行 数据模型与字段定义
domain: fund-out-transfer
kind: wiki_page
slug: payby-transfer-to-bank-data-models
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:56e8e18c-82c1-4231-b586-2130e089c7da
tags: []
---

# PayBy 转账到银行 数据模型与字段定义

本页汇总 PayBy 转账到银行账户业务（domain=payby-transfer-to-bank）涉及的公共数据结构与字段定义，覆盖订单主体、支付信息、IBAN 姓名校验、出款能力与试算结果等模型。接口调用流程见 [[payby-transfer-to-bank-overview]]，错误码见 [[payby-transfer-to-bank-return-codes]]。

## TransferToBankOrder（转账到银行订单）

转账到银行业务的核心订单对象。

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | 1581493898000 | |
| 商户订单号 | merchantOrderNo | Required | String(64) | S10000 | |
| PayBy订单号 | orderNo | Required | String(32) | O1000 | |
| 产品名称 | product | Required | String(200) | Transfer To Bank | |
| 订单状态 | status | Required | - | - | |
| 支付信息 | paymentInfo | Optional | TransferToBankPaymentInfo | - | |
| 金额 | amount | Required | Money | | |
| 受益人名称 | holderName | Required | String(64) | | 原文的sha256的值 |
| IBAN | Iban | Required | String(64) | | 原文的sha256的值 |
| SWIFT Code | swiftCode | Optional | String(11) | | |
| 付款备注 | memo | Optional | String(128) | | |
| 后台通知地址 | notifyUrl | Optional | String(200) | | |
| 错误描述 | failDes | Optional | String(200) | - | 订单失败原因 |
| 受益人地址 | beneficiaryAddress | Optional | String(200) | | 原文的sha256的值 |
| 银行关联号 | bankReference | Optional | String(128) | | v2.0.1 新增 |
| 到账金额 | fundoutAmount | Optional | Money | | |
| 汇率 | rate | Optional | BigDecimal | | |
| 金融网络 | networkCode | Required | String(16) | LOCAL | |
| 国家代码 | countryCode | Optional | String(16) | - | |
| 银行名称 | bankName | Optional | String(50) | - | |
| Fed wire账号 | fedwireCode | Optional | String(9) | - | |
| 中间行 | intermediaryBank | Optional | String(11) | - | |
| 分支行名称 | branchName | Optional | String(35) | | |
| 受益人类型 | beneficiaryType | Required | String(16) | IBAN | |

## TransferToBankPaymentInfo（支付信息）

订单中的支付附加信息。

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 付款人手续费 | payerFeeAmount | Optional | Money | |
| 预计到账时间 | arrivalTime | Optional | Timestamp(3) | 预估资金到账时间 |

## ResponseHeader（公共响应头）

所有响应 body 中的 `head` 字段。

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 请求状态 | applyStatus | Required | String(16) | SUCCESS | SUCCESS-申请成功 / FAIL-申请失败 / ERROR-申请异常 |
| 返回错误码 | code | Required | String(10) | 0 | 返回码 |
| 返回信息 | msg | Optional | String(200) | - | 返回信息 |

## OrderIndexRequest（订单查询索引）

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Optional | String(64) | T0101 | 与 orderNo 二选一，不能同时为空，且不能同时有值 |
| PayBy订单号 | orderNo | Optional | String(32) | 22000000000001 | |

## product（产品枚举）

| 产品名称 | 产品说明 |
| --- | --- |
| Transfer to bank | 转账到银行卡的产品 |

## IbanHolderName（IBAN 姓名校验结果）

用于 [[api_payby_transfer_get_iban_holder_name]] 的响应。

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 受益人掩码 | holderNameMask | Optional | String(64) | | |
| 名字比对等级 | nameMatchingLevel | Optional | String(32) | 1 | 1 - First name verification；2 - First name and last name verification；3 - Full name verification |
| 名字比对结果 | nameMatchingResult | Required | String | TRUE/FALSE | |

## FundoutAbility（出款能力）

用于 [[api_payby_transfer_get_fundout_ability_list]] 响应中的 `fundoutAbilityList` 元素。

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 收益人类型 | beneficiaryType | Required | String(20) | IBAN | IBAN / BBAN / FED_WIRE |
| 国家代码 | countryCode | Required | String(20) | UAE | |
| 到账币种 | fundoutCurrencyCode | Required | String(20) | USD | USD / AED |
| 收益人名称 | name | Required | String(20) | Local | |
| 网络代码 | networkCode | Required | String(20) | SWIFT | SWIFT / LOCAL |

## FundoutInfo（出款试算信息）

用于 [[api_payby_transfer_calculate_fundout]] 响应中 `CalculateFundoutResult.fundoutInfo`。

| 字段名 | 变量名 | 必填 | 类型 | 示例值 | 描述 |
| --- | --- | --- | --- | --- | --- |
| 手续费 | feeAmount | Required | Money | | 出款产生的出款手续费，外扣费，不包含在订单金额中 |
| 到账金额 | fundoutAmount | Required | Money | | |
| 订单金额 | orderAmount | Required | Money | | |
| 网络代码 | networkCode | Required | String(20) | SWIFT | SWIFT / LOCAL |
| 汇率 | rate | Required | BigDecimal | 1.33 | rate = fundoutAmount / orderAmount，保留 2 位小数 |

## 通用字段约定

- **货币类型 currency**：`AED` 表示阿联酋货币单位。
- **商户订单号 merchantOrderNo**：仅支持字母、数字、`-`、`_` 组合；需保持唯一；建议时间+随机序列生成；已支付或已取消的订单号不可重新发起。
- **加密字段**：`holderName`、`iban`、`beneficiaryAddress` 等敏感字段在订单中以原文 SHA256 存储；
