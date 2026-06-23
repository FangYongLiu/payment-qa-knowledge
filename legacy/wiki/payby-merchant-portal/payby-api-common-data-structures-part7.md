---
title: PayBy接口通用数据结构(Part7)
domain: merchant-portal
kind: wiki_page
slug: payby-api-common-data-structures-part7
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p7
tags: []
---

# PayBy接口通用数据结构(Part7)

本页汇总订单查询、对账单下载、分账、拒付、VAM入账、Account Funding 以及 PayFacs 子商户等接口涉及的请求/响应数据结构。相关产品类型见 [[payby-api-product-catalog]]。

## 通用响应头与订单字段

**ResponseHeader**

| 字段 | 变量 | 必填 | 类型 | 描述 |
|---|---|---|---|---|
| 请求状态 | applyStatus | Required | String(16) | SUCCESS / FAIL / ERROR |
| 返回错误码 | code | Required | String(10) | 返回码 |
| 返回信息 | msg | Optional | String(200) | - |

订单尾部补充字段：
- `payerFeeAmount` Money — 付款人手续费
- `arrivalTime` Timestamp(3) — PayBy 付款成功时间（预计到账时间）

## 订单索引与有效期更新

**OrderIndexRequest**：`merchantOrderNo`(String 64) 与 `orderNo`(String 32) 二选一，不能同时为空，也不能同时有值。

**UpdateExpiredTimeRequest**：在 OrderIndexRequest 基础上增加 `expiredTime`（Timestamp(3)，必填），用于变更订单到期时间。

## 对账单下载

**GetStatementRequest**
- `statementDate` Required String(8) 示例 `20200120` — 下载对账单的日期。

## 卡与收银台

**CardIndexRequest**：`cardToken` Required String(32)。

**GetCashierUrlInfoRequest**：`tokenUrl` Required String(200)。

## 付款人信息

**Payer**
- `mobileNumberMask` Required String(32)，示例 `+971-58**\****92` — 手机号掩码。

## 分账相关

**SharingInfo**

| 字段 | 变量 | 必填 | 类型 | 说明 |
|---|---|---|---|---|
| 分账方会员ID | sharingIdentityMid | Required | String(32) | - |
| 金额 | sharingAmount | Required | Money | - |
| 序号 | sharingIdentitySeqId | Required | Integer | 不能重复，从 1 开始连号 |
| 备注 | sharingMemo | Required | String(128) | - |
| 结算金额 | sharingSettledAmount | Optional | Money | - |
| 结算手续费金额 | sharingSettledFeeAmount | Optional | Money | - |
| 分账方代收代缴支付手续费 | withholdAndRemitFee | Optional | Boolean | - |

**SharingRemainRefundInfo**
- `memeberId` Required String(32) — 分账方会员ID
- `remainRefundAmount` Required Money — 剩余可退金额

**MemberIndex**：`memberId` Required String(32)。

## 拒付（Chargeback）

**AcquireChargeback**

| 字段 | 变量 | 类型 |
|---|---|---|
| 拒付时间 | chargebackTime | Timestamp(3) |
| 商户订单号 | merchantOrderNo | String(64) |
| PayBy订单号 | orderNo | String(32) |
| 支付金额 | payAmount | Money |
| 拒付金额 | chargebackAmount | Money |
| 案件类型 | caseType | String(200) |
| 合作方ID | partnerId | String(200) |

全部字段为 Required。

## VAM 入账订单

**VamDepositOrder**：表示一笔 VAM（虚拟账户）入账记录。

| 字段 | 变量 | 必填 | 类型 |
|---|---|---|---|
| 交易时间 | transactionTime | Required | Timestamp(3) |
| PayBy订单号 | orderNo | Required | String(32) |
| 金额 | amount | Required | Money |
| 状态 | status | Required | String(32)（如 SUCCESS） |
| referenceNo | referenceNo | Optional | String(200) |
| remitterInfo | remitterInfo | Optional | String(200) |
| senderBankCode | senderBankCode | Optional | String(200) |
| depositDetails | depositDetails | Optional | String(200) |
| collectIBAN | collectIBAN | Optional | String(200) |

## Account Funding 相关

**AccountFundingParameter**

| 字段 | 变量 | 必填 | 类型 | 说明 |
|---|---|---|---|---|
| 目的 | purpose | Required | String(20) | CRYPTOCURRENCY_PURCHASE / MERCHANT_SETTLEMENT / OTHER / PAYROLL |
| 发起方是否是收款方 | senderIsRecipient | Optional | String(10) | True / False |
| 发送类型 | senderType | Optional | String(20) | COMMERCIAL_ORGANIZATION / GOVERNMENT / NON_PROFIT_ORGANIZATION / PERSON |
| 发起方数据 | sender | Optional | SenderData | - |
| 收款方数据 | recipient | Optional | RecipientData | - |

**SenderData**：包含 `billingAddress` (BillingAddress)、`identification` (Identification)、`nameDetails` (NameDetails)，均可选。

**RecipientData**：包含 `account` (RecipientAccount)、`address` (RecipientAddress)、`identification` (Identification)、`nameDetails` (NameDetails)，均可选。

**BillingAddress**
- `city` String(100)
- `country` String(3) — ISO 3 位国家代码
- `street` String(100)

**Identification**
- `country` String(3) — ISO 3 位国家代码
- `type` String(100) — BUSINESS_TAX_ID / COMPANY_REGISTRATION_NUMBER / DATE_OF_BIRTH / EMAIL / NATIONAL_IDENTIFICATION_CARD / OTHER / PASSPORT / PHONE_NUMBER
- `value` String(50)

**NameDetails**
- `firstName` String(50)
- `lastName` String(50)
- `middleName` String(50)

**RecipientAccount**
- `fundingMethod` String(10) — DEBIT / CREDIT / CHARGE / UNKNOWN
- `identifier` String(50)
- `identifierType` String(200) — BANK_ACCOUNT_BIC / BANK_ACCOUNT_IBAN / BANK_ACCOUNT_NATIONAL / CARD_NUMBER / EMAIL_ADDRESS / OTHER / PHONE_NUMBER / SOCIAL_NETWORK_PROFILE_ID / STAGED_WALLET_USER_ID / STORED_VALUE_WALLET_USER_ID

**RecipientAddress**
- `city` String(100)
- `country` String(3) — ISO 3 位国家代码
- `postCodeZip` String(10)
- `street` String(100)
- `street2` String(100)

## PayFacs 子商户

**PayFacsSubMerchant**：用于 PayFacs 模式下传递子商户信息。

| 字段 | 变量 | 类型 | 备注 |
|---|---|---|---|
| 子商户id | identifier | String(100) | tradingName 有值时必填 |
| 注册名称 | registeredName | String(
