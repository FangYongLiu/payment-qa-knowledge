---
title: MIT/CIT 循环支付（MPGS）功能概览
domain: authorization-protocol
kind: wiki_page
slug: mit-cit-recurring-payment-overview
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:8d7a8617-1740-4670-8898-b035d5fdf23c
tags: []
---

# MIT/CIT 循环支付（MPGS）功能概览

本页介绍 PayBy 通过引入 MPGS 通道，为外部商户提供 tokenized（循环）支付能力的背景、价值与方案要点。

## 背景

- 业务团队希望为外部大商户提供 tokenized（recurring）支付能力，以提升整体支付成功率。
- 目前 CKO 通道的 tokenized 支付仅支持 Botim 业务。
- 引入 MPGS 通道，扩展对其他外部商户的 tokenized 支付支持。
- 关联需求：MER-413 Recurring Payments (CIT/MIT)、MIT/CIT Second Phase、MIT/CIT Via MPGS；关联 Jira：PAYM-2235、PAYM-1558。

## Tokenized 支付的优势

- 后续交易（MIT）无需再触发 3DS 认证，成功率更高。
- 相较 MOTO 支付，拒付（chargeback）争议的胜率更高。

## 总体方案要点

- 通道：在原有 CKO 之外，新增 MPGS 作为 tokenized 循环支付通道。
- 协议签约（CIT）：首笔交易完成 3DS 认证并签约后，生成可复用的 `deduct_protocol_no` 与 card token。
- 后续扣款（MIT）：基于已签约协议与 card token，通过商户侧发起 AutoDebit，无需再次 3DS。
- 关键数据落地：
  - `deduct.t_deduct_protocol`：协议数据，CIT 成功后状态置为 `Y`。
  - `member.tr_bank_card_token`：当 `institution_code='MPGS'` 且 `status='Y'` 表示 MPGS token 已建立。
  - `acquireii.t_card_info` / `member.tr_bank_account`：可查询 `card_token` / `OUT_ACCOUNT_TOKEN`。
- 与 MPGS 的交互：在请求体中携带 `agreement`（含 `id`、`type=RECURRING`、`expiryDate`、`numberOfPayments`、`amountVariability`、`paymentFrequency`、`minimumDaysBetweenPayments`）以及 `sourceOfFunds`、`transaction.source=INTERNET` 等字段。

## 支持的支付场景

- `paySceneCode=PAYANDSIGN`：PayPage 内通过 PayBy/Botim App 完成首次签约支付（CIT）。
- `paySceneCode=DIRECTPAY`（首笔 CIT）：携带卡信息（FPN/DPN）、`agreementInfo` 与 `customerId`。
- `paySceneCode=DIRECTPAY`（后续 CIT）：以 `cardToken` + `agreementInfo` 复用已签约关系，`source=INTERNET`。
- `paySceneCode=AUTODEBIT`（MIT）：以 `authProtocolNo` + `source=MERCHANT` 发起商户侧自动扣款。

## 通道路由与触发条件

- CIT 路由要求：触发 3DS 验证，且路由至 MPGS（或 PAYANDSIGN 场景下路由至 cko/mpgs）通道。
- 路由控制配置（ACS）：
  - `prarmKey=DEDUCT_INTERNAL_PARTNER`，`paramValue=Y`，按 `MerchantId` 配置。
- 必须开通的产品：Auto Debit、Direct Pay Domestic Card、Direct Pay INTL Card。

## 协议与 Token 状态规则

- CIT 成功后，`t_deduct_protocol` 会新增一条 `status=Y` 的协议数据。
- 多次 CIT 成功的处理：
  - CKO 通道：旧协议数据状态会被置为 `F`。
  - MPGS 通道：会生成新的协议数据。
- MPGS token 校验：`tr_bank_card_token` 中 `institution_code='MPGS'` 且 `status='Y'`。

## 相关链接

- 测试场景与执行步骤详见 [[scn_mit_cit_test_guide]]。
