---
title: 商户出款业务总览
domain: withdraw-cash
kind: wiki_page
slug: merchant-fund-out-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:dc3fae70-d705-4a94-aecf-3cb16c6b7c7a
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

### 提现流程（移动端）

提现流程在移动端 App 的 "Withdraw funds" 页面完成，主要步骤：

1. **进入提现页**：展示当前可用余额（如 `Balance: ⩾104.68` AED）。
2. **输入金额**：用户在金额输入框输入提现金额，支持快捷金额按钮（`50`、`100`、`Max`），并提供 `View limit` 查看额度链接。
3. **选择提现目的地**（Select withdrawal destination）：列出可用的出款通道，例如：
   - `Aani`：标记为 `Recommended`，到账时效 `Instant`，手续费 `D2.00`
4. **提交提现**：完成后弹出 "Withdrawal Successful" 确认弹层，展示：
   - `Transaction ID`（交易流水号，例如 `311774263675574883`）
   - `Okay` 按钮关闭弹层

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
