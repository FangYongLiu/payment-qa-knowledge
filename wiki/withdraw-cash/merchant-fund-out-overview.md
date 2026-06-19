---
title: 商户出款业务总览
domain: withdraw-cash
kind: wiki_page
slug: merchant-fund-out-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:725e7e15-a17e-474d-88b0-41b03052130e
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

### 提现流程示例（Botim / Transfer to Bank Account）

以 Botim 钱包内 "Transfer to Bank Account" 为例，提现页关键元素：

- 顶部展示可用余额，例如 `Balance: 865.62 AED`，带 info 图标
- 金额输入框（币种 AED / د.إ），支持快捷金额按钮（如 `500`、`Max`）
- `View limit` 链接，用于查看限额
- "Choose your withdrawal method" 区块，列出可选出款方式

提现方式示例：

- **Aani**（标记 `Recommended`）
  - 到账时效：`Instant`
  - 手续费：`AED 0.50`

提交成功后弹出确认弹窗：

- 标题：`Withdrawal Successful`
- 文案：`Your bank might need up to 5 working days to process the withdrawal.`
- 主按钮：`Okay`

即：用户侧虽提示瞬时（Instant）出款，但银行入账实际可能耗时最多 5 个工作日。

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

## 涉及的应用

- `gp083_merchant-fundout`
- `gp012_fundout`
- `gp156_exchange`
- `cmf`
- `router`
