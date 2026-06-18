---
title: 商户出款业务总览
domain: merchant-fund-out
kind: wiki_page
slug: merchant-fund-out-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:d24969b4-625e-4ea0-b20d-669043b3a083
tags: []
---

# 商户出款业务总览

商户出款业务覆盖**商户提现**、**出款到卡**、**出款到账户**三种场景，分别对应不同的产品集、SGS 接口与底层数据表。详见 [[flow_merchant_fund_out]]。

## 商户提现

- **产品集**：默认开通（无需额外开通）
- **关键能力**：绑卡、提现
- **相关表**：
  - 绑卡：`member.tr_beneficiary_info`
  - 提现：`mhtfundout.t_withdraw_order`

## 商户出款到卡

- **产品集**：Transfer
- **SGS 接口**：`transfer/placeTransferToBankOrder`（详见 [[api_transfer_place_transfer_to_bank_order]]）
- **接口文档**：https://developers.payby.com/docs/Transfer%20to%20bank/transfer-to-bank
- **重要参数**：
  - `swiftCode`：如 `BBMEAEAD`
  - `iban`：加密，如 `AE470200000012213138001`
  - `holderName`：加密持卡人姓名
  - `networkCode`：如 `LOCAL`
  - `countryCode`：如 `UAE`
  - `fundoutCurrencyCode`：如 `AED`
  - `beneficiaryType`：如 `IBAN`
  - `beneficiaryAddress`：加密收款人地址
- **相关表**：
  - `mhtfundout.t_fundout_bankcard_order`
  - `mhtfundout.t_fundout_bankcard_beneficiary`
  - `mhtfundout.t_account_beneficiary_history`
- **商户控台**：商户控台提供出款到卡入口

## 商户出款到账户

- **产品集**：
  - Transfer to bank
  - Transfer To Bank Via SWIFT（通过 SWIFT 网络出款）
  - Transfer To Bank Via FEDWIRE（通过 FEDWIRE 网络出款）
- **SGS 接口**：`transfer/placeTransferOrder`（详见 [[api_transfer_place_transfer_order]]）
- **接口文档**：https://developers.payby.com/docs/Transfer/
- **重要参数**：
  - `amount`：含 `currency`（如 `AED`）与 `amount`（如 `500`）
  - `beneficiaryIdentity`：加密，如 `+971-585920614`
  - `beneficiaryIdentityType`：如 `PHONE_NO`
- **相关表**：`mhtfundout.t_fundout_account_order`
- **商户控台**：商户控台提供出款到账户入口

## 涉及的应用

- `gp083_merchant-fundout`
- `gp012_fundout`
- `gp156_exchange`
- `cmf`
- `router`
