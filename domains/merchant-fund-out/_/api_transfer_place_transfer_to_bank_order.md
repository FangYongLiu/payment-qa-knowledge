---
id: api_transfer_place_transfer_to_bank_order
object_type: API
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:d24969b4-625e-4ea0-b20d-669043b3a083
tags:
- Transfer
- fundout
- bankcard
subdomain: null
module: null
sensitivity: normal
name: 出款到银行卡接口
aliases:
- transfer/placeTransferToBankOrder
related_services: []
related_tables:
- mhtfundout.t_fundout_bankcard_order
- mhtfundout.t_fundout_bankcard_beneficiary
- mhtfundout.t_account_beneficiary_history
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
商户出款到银行卡接口，所属产品集 Transfer，用于将资金通过银行渠道出款至指定收款人银行卡/IBAN。

## 路径/方法
- SGS: `transfer/placeTransferToBankOrder`
- 接口文档: https://developers.payby.com/docs/Transfer%20to%20bank/transfer-to-bank

## 入参
重要参数：
- `swiftCode`: "BBMEAEAD"
- `iban`: 加密｜如 "AE470200000012213138001"
- `holderName`: 加密｜如 "CAN WANG"
- `networkCode`: "LOCAL"
- `countryCode`: "UAE"
- `fundoutCurrencyCode`: "AED"
- `beneficiaryType`: "IBAN"
- `beneficiaryAddress`: 加密｜如 "sigma 1 tower"

## 出参
原文未提供。

## 错误码
原文未提供。

## 测试校验点
- 加密字段（`iban`、`holderName`、`beneficiaryAddress`）按规则加密传入
- `networkCode`=LOCAL、`countryCode`=UAE、`fundoutCurrencyCode`=AED 与 `swiftCode` 配置一致
- `beneficiaryType`=IBAN 时 `iban` 必填且格式正确
- 落库表校验：
  - `mhtfundout.t_fundout_bankcard_order`（订单）
  - `mhtfundout.t_fundout_bankcard_beneficiary`（收款人）
  - `mhtfundout.t_account_beneficiary_history`（收款人历史）
- 商户控台可见对应出款到卡记录
