---
title: PayBy转账到银行账户接口总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p1
tags: []
---

# PayBy转账到银行账户接口总览

本页汇总 PayBy 转账到银行账户接口的版本变更、术语、协议规则、参数规范及通用数据结构定义，作为接入文档的总览索引。

## 阅读对象

面向接入 PayBy 的商户系统（在线购物平台、人工/自动化收银系统等）的：
- 技术架构师
- 研发工程师
- 测试工程师
- 系统运维工程师

## 版本说明

| 版本 | 时间 | 修改点 |
| --- | --- | --- |
| v2.0.0 | 2021-10-12 | 初稿 |
| v2.0.1 | 2021-12-02 | 新增 `bankReference` |
| v2.1   | 2022-03-01 | 增加国际汇款通道；增加出款能力查询接口；增加试算接口 |
| v2.2   | 2024-08-20 | 增加 IBAN 查询姓名接口 |
| v2.3   | 2024-12-11 | 单笔付款到银行卡接口增加 `cityCode` |
| v2.4   | 2025-02-19 | 单笔付款到银行卡接口增加 `purposeCode` |

## 术语

- **PayBy支付系统**：PayBy 支付流程涉及的 API 接口、后台业务处理系统、回调通知等系统的总称。

## 协议规则

商户接入 PayBy 调用 API 必须遵守：

| 方式 | 说明 |
| --- | --- |
| 传输方式 | HTTPS |
| 提交方式 | POST |
| 数据格式 | JSON |
| 字符编码 | UTF-8 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应数据都需要签名 |

> 签名/加密的具体规则与密钥生成方式详见 [[payby-transfer-to-bank-security]]。

## 参数规定

### 请求参数

- 请求参数的值为空时不予处理。

### 货币类型 currency

| Currency | 说明 |
| --- | --- |
| AED | 阿联酋货币单位 |

### 商户订单号 merchantOrderNo

- 由商户自定义生成，仅支持字母、数字、`-`、`_` 的组合。
- 必须保持唯一性（建议根据系统时间 + 随机序列生成）。
- 重新发起一笔支付应使用原订单号，避免重复支付。
- 已支付或已调用取消交易的订单号不能重新发起支付。

## 通用数据结构

### TransferToBankOrder

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | |
| 商户订单号 | merchantOrderNo | Required | String(64) | |
| PayBy订单号 | orderNo | Required | String(32) | |
| 产品名称 | product | Required | String(200) | 例：Transfer To Bank |
| 订单状态 | status | Required | | |
| 支付信息 | paymentInfo | Optional | TransferToBankPaymentInfo | |
| 金额 | amount | Required | Money | |
| 受益人名称 | holderName | Required | String(64) | 原文的 sha256 值 |
| IBAN | Iban | Required | String(64) | 原文的 sha256 值 |
| SWIFT Code | swiftCode | Optional | String(11) | |
| 付款备注 | memo | Optional | String(128) | |
| 后台通知地址 | notifyUrl | Optional | String(200) | |
| 错误描述 | failDes | Optional | String(200) | 订单失败原因 |
| 受益人地址 | beneficiaryAddress | Optional | String(200) | 原文的 sha256 值 |
| 银行关联号 | bankReference | Optional | String(128) | v2.0.1 新增 |
| 到账金额 | fundoutAmount | Optional | Money | |
| 汇率 | rate | Optional | BigDecimal | |
| 金融网络 | networkCode | Required | String(16) | 例：LOCAL |
| 国家代码 | countryCode | Optional | String(16) | |
| 银行名称 | bankName | Optional | String(50) | |
| Fed wire账号 | fedwireCode | Optional | String(9) | |
| 中间行 | intermediaryBank | Optional | String(11) | |
| 分支行名称 | branchName | Optional | String(35) | |
| 受益人类型 | beneficiaryType | Required | String(16) | 例：IBAN |
| purposeCode | purposeCode | Optional | String(16) | 例：COM |

### purposeCode 枚举

| name | description |
| --- | --- |
| COM | Commission |
| FIS | Financial services |
| GDS | Goods Bought or Sold |
| GMS | Processing repair and maintenance services on goods |
| GOS | Government goods and services embassies etc. |
| GRI | Government related income taxes, tariffs, capital transfers, etc. |
| IFS | Information services |
| IGT | Inter group transfer |
| INS | Insurance services |
| ITS | Computer services |
| OAT | Own account transfer |

### TransferToBankPaymentInfo

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 付款人手续费 | payerFeeAmount | Optional | Money | |
| 预计到账时间 | arrivalTime | Optional | Timestamp(3) | 预估资金到账时间 |

### ResponseHeader

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求状态 | applyStatus | Required | String(16) | SUCCESS-申请成功；FAIL-申请失败；ERROR-申请异常 |
| 返回错误码 | code | Required | String(10) | |
| 返回信息 | msg | Optional | String(200) | |

### OrderIndexRequest

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Optional | String(64) | 与 orderNo 二选一，不能同时为空且不能同时有值 |
| PayBy订单号 | orderNo | Optional | String(32) | |

### product

| 产品名称 | 产品说明 |
| --- | --- |
| Transfer to bank | 转账到银行卡的产品 |

### IbanHolderName

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 受益人掩码 | holderNameMask | Optional | String(64) | |
| 名字比对等级 | nameMatchingLevel | Optional | String(32) | 1 - First name verification；2 - First name and last name verification；3 - Full name verification |
| 名字比对结果 | nameMatchingResult | Required | String | TRUE/FALSE |

## API 列表

- [[api_transfer_get_iban_holder_name]]：校验用户名称与 IBAN 账号是否匹配（v2.2 起支持）。
- [[api_transfer_get_fundout_ability_list]]：查询商户可出款
