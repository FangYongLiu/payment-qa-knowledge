---
title: 商户出款业务总览
domain: fund-out-transfer
kind: wiki_page
slug: merchant-fund-out-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b8209e2b-befd-4e6d-a82a-4e7759b5ef81
tags: []
---

# 商户出款业务总览

商户出款业务（domain: `merchant-fund-out`）覆盖商户将资金转出至外部银行卡或账户的场景，包含商户提现、出款到卡、出款到账户等产品形态。

## 业务范围

商户出款业务包含以下两大产品集方向：

- **出款到卡**：将资金出款至指定银行卡（IBAN 等），详见 [[scn_fundout_to_bankcard]]
- **出款到账户**：将资金出款至账户标识（手机号等），详见 [[scn_fundout_to_account]]

## 商户提现

- 产品集：默认开通
- 绑卡数据表：`member.tr_beneficiary_info`
- 提现数据表：`mhtfundout.t_withdraw_order`

## 商户出款到卡

- 产品集：`Transfer`
- SGS 接口：`transfer/placeTransferToBankOrder`
- 接口文档：https://developers.payby.com/docs/Transfer%20to%20bank/transfer-to-bank

重要参数示例：

```json
"swiftCode": "BBMEAEAD",
"iban": "加密|AE470200000012213138001",
"holderName": "加密|CAN WANG",
"networkCode": "LOCAL",
"countryCode": "UAE",
"fundoutCurrencyCode": "AED",
"beneficiaryType": "IBAN",
"beneficiaryAddress": "加密|sigma 1 tower"
```

涉及数据表：

- `mhtfundout.t_fundout_bankcard_order`
- `mhtfundout.t_fundout_bankcard_beneficiary`
- `mhtfundout.t_account_beneficiary_history`

支持在商户控台进行操作。详见 [[scn_fundout_to_bankcard]]。

## 商户出款到账户

- 产品集：
  - `Transfer to bank`
  - `Transfer To Bank Via SWIFT`（通过 SWIFT 网络出款）
  - `Transfer To Bank Via FEDWIRE`（通过 FEDWIRE 网络出款）
- SGS 接口：`transfer/placeTransferOrder`
- 接口文档：https://developers.payby.com/docs/Transfer/

重要参数示例：

```json
{
  "amount": {
    "currency": "AED",
    "amount": 500
  },
  "beneficiaryIdentity": "加密|+971-585920614",
  "beneficiaryIdentityType": "PHONE_NO"
}
```

涉及数据表：

- `mhtfundout.t_fundout_account_order`

支持在商户控台进行操作。详见 [[scn_fundout_to_account]]。

## C 端转账场景（Botim Transfer）

C 端用户在 Botim 内发起转账时，会出现支付方式选择面板（payment method selection bottom sheet），用于选择资金来源（funding source）。

典型 UI 元素：

- 顶部展示金额与用途，例如 `AED 1.00` / `Transfer`
- 支付方式列表（单选），每项包含图标、标签与右侧单选按钮：
  - **botim pay**：站内钱包，展示余额（如 `AED 363.62`），通常默认选中
  - **Apple Pay**
  - **Debit Card**：展示卡号末四位（如 `3250`、`6789`），区分 VISA / Mastercard
  - **Credit Card**：若该服务不支持，则展示 `Unavailable for this service` 并置灰禁用
- `Add payment method`：新增支付方式入口
- 主操作按钮：`Pay`

转账成功后，会话流中显示转账卡片，包含金额（如 `AED 125.00`）、状态 `Transferred - Oct 12`、来源标记 `Botim transfer` 与时间。

## 涉及的应用

- `gp083_merchant-fundout`
- `gp012_fundout`
- `gp156_exchange`
- `cmf`
- `router`
