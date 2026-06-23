---
title: 商户出款业务总览
domain: fund-out-transfer
kind: wiki_page
slug: merchant-fund-out-overview
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:bd547fc3-fbc0-4472-b7b5-54175ab1e278
tags: []
---

# 商户出款业务总览

商户出款业务（domain: `merchant-fund-out`）覆盖商户将资金转出至外部银行卡或账户的场景，包含商户提现、出款到卡、出款到账户等产品形态。

## 业务范围

商户出款业务包含以下两大产品集方向：

- **出款到卡**：将资金出款至指定银行卡（IBAN 等），详见 [[scn_fundout_to_bankcard]]
- **出款到账户**：将资金出款至账户标识（手机号、Botim 联系人、Aani 等），详见 [[scn_fundout_to_account]]

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

### Botim 端 Send money 出款渠道

在 Botim app 端 "Send money" 入口，用户可输入金额（支持快捷金额 `100` / `200` / `500` / `1000`，币种 AED）并选择以下三种出款渠道（rail）：

| 渠道 | 说明 | 费用 |
| --- | --- | --- |
| **Botim** | Instant to any botim contact（即时转账给任意 Botim 联系人） | Free |
| **Aani** | Instant to any Aani phone number（即时转账至任意 Aani 手机号） | AED 0.5（当前免收，划线展示） |
| **International transfer** | Fast at top rates to 150+ countries（国际汇款，覆盖 150+ 国家） | AED 0 |

操作流程：输入金额 → 选择出款渠道（Botim 联系人 / Aani / International）→ 点击 `Send` 提交。

## 涉及的应用

- `gp083_merchant-fundout`
- `gp012_fundout`
- `gp156_exchange`
- `cmf`
- `router`
