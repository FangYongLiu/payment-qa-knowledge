---
title: MIT/CIT MPGS 测试指南
domain: authorization-protocol
kind: wiki_page
slug: mit-cit-mpgs-test-guide
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2095087700
tags: []
---

# MIT/CIT MPGS 测试指南

本页介绍通过 MPGS 通道实现 tokenized recurring payment 的背景、前置配置，以及四类 CIT/MIT 场景的测试方法。

## 背景

为提升整体支付成功率，业务侧计划向外部大商户提供 tokenized（recurring）支付能力。由于 CKO 的 tokenized payment 目前仅支持 Botim 业务，因此引入 MPGS 通道为其他外部商户开放该能力。

Tokenized 支付的优势：
- 后续交易无需 3DS 认证，成功率更高。
- 相比 MOTO 支付，chargeback 争议的胜诉率更高。

## 前置条件

### ACS 配置
为测试商户在 ACS 上添加配置：
- `MerchantId`: your test mid
- `prarmKey`: `DEDUCT_INTERNAL_PARTNER`
- `paramValue`: `Y`

### 开通产品
- Auto Debit
- Direct Pay Domestic Card
- Direct Pay INTL Card

## 四类测试场景

按 CIT（Customer Initiated Transaction）/ MIT（Merchant Initiated Transaction）划分：

- [[scn_mit_cit_payandsign]]：通过 PayPage + payby/botim app 完成签约支付，触发 3DS，路由至 cko/mpgs。
- [[scn_mit_cit_directpay_first]]：使用卡信息（FPN/DPN）+ `agreementInfo` + `customerId` 创建 DirectPay 首次 CIT，触发 3DS，路由至 mpgs。
- [[scn_mit_cit_directpay_subsequent]]：使用 `cardToken` + `agreement id` 创建 `source=INTERNET` 的 DirectPay 后续 CIT。
- [[scn_mit_autodebit]]：使用 `authProtocolNo` + `source=MERCHANT` 创建 AutoDebit 完成 MIT 代扣。

## 通用校验点

各 CIT 场景成功后，通过以下方式验证：

### 协议数据
```sql
select * from deduct.t_deduct_protocol
 where partner_id=200000054800 and status="A"
 order by create_time desc;
```
CIT 成功后会新增一条记录，`status = 'Y'`，可获取 `deduct_protocol_no` 用于后续 MIT。
- CKO 通道多次 CIT 成功：旧数据 status 置为 `F`。
- MPGS 通道多次 CIT 成功：会新增数据。

### 卡 Token
```sql
select * from member.tr_bank_card_token
 where institution_code='MPGS' and status='Y'
 order by create_time desc;
```

### MPGS 报文日志
日志中应包含发送给 MPGS 的 `agreement` 字段，例如 `BankClientImpl` 输出的请求体含：
- `agreement.type=RECURRING`
- `agreement.id`、`expiryDate`、`numberOfPayments`、`amountVariability`、`minimumDaysBetweenPayments`、`paymentFrequency`
- `apiOperation=PAY`，`sourceOfFunds.provided.card.storedOnFile=TO_BE_STORED`
- `transaction.source=INTERNET`，并带 `authentication.transactionId`

### 获取 cardToken
后续 CIT 需要的 `cardToken` 可从以下表取得：
```sql
select card_token from acquireii.t_card_info where global_id={global_id};
select OUT_ACCOUNT_TOKEN from member.tr_bank_account
 where MEMBER_ID={mid} and STATUS=1 order by create_time desc;
```
