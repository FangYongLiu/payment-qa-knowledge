---
title: PayBy转账到银行账户接口总览
domain: payby-bank-transfer
kind: wiki_page
slug: payby-bank-transfer-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-bankcard-v0.2-p1
tags: []
---

# PayBy转账到银行账户接口总览

本页汇总 PayBy 转账到银行账户接口的总体接入规范，包括文档说明、版本历史、术语、协议规则、参数规范以及签名与加密算法。具体接口请参见 [[api_payby_verify_bank_card_payout_eligibility]]。

## 文档说明

### 阅读对象

商户系统（在线购物平台、人工收银系统、自动化智能收银系统或其他）集成 PayBy 涉及的：

- 技术架构师
- 研发工程师
- 测试工程师
- 系统运维工程师

### 版本说明

| 版本 | 时间 | 修改点 |
| --- | --- | --- |
| v0.1 | 2025-03-22 | 初稿 |
| v0.2 | 2025-05-19 | 1. 单笔转账银行卡接口新增请求参数 `cardToken` 和 `last4`；2. 单笔转账银行卡接口新增返回参数 `cardToken`；3. 单笔转账银行卡接口新增请求参数 `countryCode`、`state`、`zipCode`、`city`、`addressLine`；4. 验证银行卡接口新增请求参数 `cardToken` 和 `last4`；5. 验证银行卡接口新增请求参数 `cardTokenMerchantId`；6. 单笔转账银行卡接口新增返回参数 `cardTokenMerchantId` |

## 术语

### PayBy 支付系统

完成 PayBy 支付流程中涉及的 API 接口、后台业务处理系统、回调通知等系统的总称。

## 协议规则

商户接入 PayBy 支付系统调用 API 必须遵守：

| 方式 | 说明 |
| --- | --- |
| 传输方式 | 为保证交易安全，采用 HTTPS 传输 |
| 提交方式 | 采用 POST 方法提交 |
| 数据格式 | JSON |
| 字符编码 | 统一采用 UTF-8 |
| 签名算法 | SHA256WithRSA |
| 签名要求 | 请求和响应数据都需要签名 |

## 参数规范

### 请求参数规定

- 如果请求参数的值为空，则不予处理。

### 货币类型（currency）

| Currency | 说明 |
| --- | --- |
| AED | 阿联酋货币单位 |

### 商户订单号（merchantOrderNo）

- 由商户自定义生成，仅支持字母、数字、中划线 `-`、下划线 `_` 的英文半角组合。
- PayBy 要求商户订单号保持唯一性（建议根据当前系统时间加随机序列生成）。
- 重新发起一笔支付要使用原订单号，避免重复支付。
- 已支付过或已调用取消交易的订单号不能重新发起支付。

### product

| 产品名称 | 产品说明 |
| --- | --- |
| Transfer Bank Card | - |

### TransferBankCardOrder

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求时间 | requestTime | Required | Timestamp(3) | |
| 商户订单号 | merchantOrderNo | Required | String(64) | |
| PayBy订单号 | orderNo | Required | String(32) | |
| 产品名称 | product | Required | String(200) | Transfer Bank Card |
| 订单状态 | status | Required | - | |
| 金额 | amount | Required | Money | |
| 账户持有人类型 | accountHolderType | Required | String(16) | INDIVIDUAL / CORPORATE |
| firstName | firstName | Optional | String(200) | 原文 sha256，INDIVIDUAL 时必输 |
| lastName | lastName | Optional | String(200) | 原文 sha256，INDIVIDUAL 时必输 |
| middleName | middleName | Optional | String(200) | 原文 sha256 |
| 公司名称 | companyName | Optional | String(200) | 原文 sha256，CORPORATE 时必输 |
| cardNumber | cardNumber | Optional | String(64) | 原文 sha256 |
| cardToken | cardToken | Optional | String(32) | |
| cardTokenMerchantId | cardTokenMerchantId | Optional | String(32) | |
| 失效月 | expiryMonth | Required | String(2) | |
| 失效年 | expiryYear | Required | String(4) | |
| 付款备注 | memo | Optional | String(128) | |
| 后台通知地址 | notifyUrl | Optional | String(200) | |
| 错误描述 | failDes | Optional | String(200) | 订单失败原因 |
| 银行关联号 | bankReference | Optional | String(128) | |
| 付款人手续费 | payerFeeAmount | Required | Money | |
| 手续费支付方 | payerFeeMemberId | Required | String(32) | 手续费支付方 ID |
| 扣款时间 | paidTime | Required | Date | |
| 退款时间 | refundedTime | Optional | Date | |
| 国家代码 | countryCode | Required | String(2) | 两位 ISO 国家代码 |
| state | state | Optional | String(3) | AU/CA/US 必输 |
| zip code | zipCode | Optional | String(10) | SA 必输 |
| city | city | Required | String(50) | |
| address line | addressLine | Required | String(200) | |
| SenderInfo | senderInfo | Optional | SenderInfo | INDIVIDUAL 时必输 |
| senderType | senderType | Required | String(16) | INDIVIDUAL / CORPORATE |

### SenderInfo

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| firstName | firstName | Required | String(50) | 原文 sha256 |
| lastName | lastName | Required | String(50) | 原文 sha256 |
| 国家代码 | countryCode | Required | String(2) | 两位 ISO 国家代码 |
| state | state | Optional | String(3) | US 必输 |
| zip code | zipCode | Optional | String(10) | US 必输 |
| city | city | Required | String(50) | |
| address line | addressLine | Required | String(200) | |
| reference | reference | Required | String(15) | 发送人唯一标识（如客户号），仅字母数字，5–15 字符 |
| source of funds | sourceOfFunds | Required | String(15) | Enum: `credit`、`debit`、`prepaid`、`deposit_account`、`mobile_money_account`、`cash` |
| date of birth | dateOfBirth | Optional | String(10) | YYYY-MM-DD，跨境转账必输 |

### ResponseHeader

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 请求状态 | applyStatus | Required | String(16) | SUCCESS-申请成功 / FAIL-申请失败 / ERROR-申请异常 |
| 返回错误码 | code | Required | String(10) | 返回码 |
| 返回信息 | msg | Optional | String(200) | 返回信息 |

### OrderIndexRequest

| 字段名 | 变量名 | 必填 | 类型 | 描
