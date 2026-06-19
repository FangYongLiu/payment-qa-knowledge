---
id: flow_merchant_fund_out
object_type: Flow
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:d24969b4-625e-4ea0-b20d-669043b3a083
tags:
- withdraw
- transfer-to-bank
- transfer-to-account
subdomain: null
module: null
sensitivity: normal
name: 商户出款端到端流程
aliases: []
related_services:
- gp083_merchant-fundout
- gp012_fundout
- gp156_exchange
- cmf
- router
related_tables:
- mhtfundout.t_withdraw_order
- mhtfundout.t_fundout_bankcard_order
- mhtfundout.t_fundout_bankcard_beneficiary
- mhtfundout.t_account_beneficiary_history
- mhtfundout.t_fundout_account_order
- member.tr_beneficiary_info
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
商户出款端到端业务覆盖三类场景：商户提现、商户出款到银行卡、商户出款到账户。不同场景对应不同的产品集与 SGS 接口，最终通过 gp083_merchant-fundout、gp012_fundout、gp156_exchange、cmf、router 等应用协同完成出款。

## 步骤(跨系统)
### 1. 商户提现
- 产品集：默认开通
- 绑卡：受益人信息写入 `member.tr_beneficiary_info`
- 提现：订单写入 `mhtfundout.t_withdraw_order`

### 2. 商户出款到卡
- 产品集：Transfer
- SGS 接口：`transfer/placeTransferToBankOrder`
- 接口文档：https://developers.payby.com/docs/Transfer%20to%20bank/transfer-to-bank
- 重要参数：
  - `swiftCode`: BBMEAEAD
  - `iban`: 加密|AE470200000012213138001
  - `holderName`: 加密|CAN WANG
  - `networkCode`: LOCAL
  - `countryCode`: UAE
  - `fundoutCurrencyCode`: AED
  - `beneficiaryType`: IBAN
  - `beneficiaryAddress`: 加密|sigma 1 tower
- 落表：
  - `mhtfundout.t_fundout_bankcard_order`
  - `mhtfundout.t_fundout_bankcard_beneficiary`
  - `mhtfundout.t_account_beneficiary_history`
- 入口：商户控台

### 3. 商户出款到账户
- 产品集：Transfer to bank、Transfer To Bank Via SWIFT(通过 swift 网络出款)、Transfer To Bank Via FEDWIRE(通过 fedwire 网络出款)
- SGS 接口：`transfer/placeTransferOrder`
- 接口文档：https://developers.payby.com/docs/Transfer/
- 重要参数：
  - `amount.currency`: AED
  - `amount.amount`: 500
  - `beneficiaryIdentity`: 加密|+971-585920614
  - `beneficiaryIdentityType`: PHONE_NO
- 落表：`mhtfundout.t_fundout_account_order`
- 入口：商户控台

## 涉及服务/表
- 应用：
  - gp083_merchant-fundout
  - gp012_fundout
  - gp156_exchange
  - cmf
  - router
- 表：
  - `member.tr_beneficiary_info`
  - `mhtfundout.t_withdraw_order`
  - `mhtfundout.t_fundout_bankcard_order`
  - `mhtfundout.t_fundout_bankcard_beneficiary`
  - `mhtfundout.t_account_beneficiary_history`
  - `mhtfundout.t_fundout_account_order`
- 关联接口：[[api_transfer_place_transfer_to_bank_order]]、[[api_transfer_place_transfer_order]]
- 业务总览：[[merchant-fund-out-overview]]

## 校验点
- 商户提现需开通默认产品集，绑卡信息正确写入 `member.tr_beneficiary_info`，提现订单写入 `mhtfundout.t_withdraw_order`
- 出款到卡需开通 Transfer 产品集；关键字段(swiftCode/iban/holderName/networkCode/countryCode/fundoutCurrencyCode/beneficiaryType/beneficiaryAddress)按要求加密；订单与受益人正确落入 `t_fundout_bankcard_order`、`t_fundout_bankcard_beneficiary`、`t_account_beneficiary_history`
- 出款到账户需根据网络开通对应产品集(Transfer to bank / SWIFT / FEDWIRE)；`beneficiaryIdentity` 加密、`beneficiaryIdentityType` 与币种金额正确传递；订单落入 `t_fundout_account_order`
