---
id: flow_merchant_fundout
object_type: Flow
name: 商户出款端到端流程 (Merchant Fund-Out)
aliases: [商户出款, merchant fund out, 商户提现/出款到卡/出款到账户]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki:d24969b4-625e-4ea0-b20d-669043b3a083 (+ confluence:AQ/1012367385)
tags: [online-business, fundout, 出款, 提现, transfer-to-bank, transfer-to-account]
related_services: [svc_merchant_fundout, svc_fundout]
related_tables: [tbl_mhtfundout_t_fundout_bankcard_order, tbl_mhtfundout_t_fundout_order]
related_scenarios: [scn_online_business_merchant_payout]
---

# 商户出款端到端流程 (Merchant Fund-Out)

## 概述
商户出款覆盖三类场景:**商户提现**、**出款到银行卡**、**出款到账户**。不同场景对应不同产品集与 SGS 接口,经 [[svc_merchant_fundout]]、[[svc_fundout]] 与 exchange / cmf / router 等应用协同完成出款。入口为商户控台。

## 步骤(跨系统)
### 1. 商户提现
- 产品集:默认开通。
- 绑卡:受益人信息写入 `member.tr_beneficiary_info`(表对象待补)。
- 提现:订单写入 `mhtfundout.t_withdraw_order`(表对象待补)。

### 2. 出款到银行卡
- 产品集:Transfer。
- SGS 接口:`transfer/placeTransferToBankOrder`(接口文档 developers.payby.com/docs/Transfer to bank)。
- 关键参数(部分加密):`swiftCode`=BBMEAEAD、`iban`(加密)、`holderName`(加密)、`networkCode`=LOCAL、`countryCode`=UAE、`fundoutCurrencyCode`=AED、`beneficiaryType`=IBAN、`beneficiaryAddress`(加密)。
- 落表:[[tbl_mhtfundout_t_fundout_bankcard_order]];受益人 `t_fundout_bankcard_beneficiary` / `t_account_beneficiary_history`(表对象待补)。

### 3. 出款到账户
- 产品集:Transfer to bank / Transfer To Bank Via SWIFT / Transfer To Bank Via FEDWIRE。
- SGS 接口:`transfer/placeTransferOrder`(接口文档 developers.payby.com/docs/Transfer)。
- 关键参数:`amount.currency`=AED、`amount.amount`、`beneficiaryIdentity`(加密)、`beneficiaryIdentityType`=PHONE_NO。
- 落表:`mhtfundout.t_fundout_account_order`(表对象待补);通用出款单见 [[tbl_mhtfundout_t_fundout_order]]。

## 关联关系
- **经过的服务(有序)**:[[svc_merchant_fundout]] → [[svc_fundout]] →(exchange / cmf / router,这些服务在本域外或对象待补)(= `related_services`)。
- **关键表**:[[tbl_mhtfundout_t_fundout_bankcard_order]]、[[tbl_mhtfundout_t_fundout_order]](= `related_tables`);`t_withdraw_order` / `t_fundout_account_order` / `t_fundout_bankcard_beneficiary` / `t_account_beneficiary_history` / `member.tr_beneficiary_info` 表对象待补。
- **关键场景**:[[scn_online_business_merchant_payout]](= `related_scenarios`,出款 / 转账场景)。

## 校验点
- 商户提现:需开通默认产品集,绑卡信息正确写入受益人表,提现订单写入 `t_withdraw_order`。
- 出款到卡:需开通 Transfer 产品集;关键字段按要求加密;订单与受益人正确落入银行卡出款单与受益人表。
- 出款到账户:按网络开通对应产品集(Transfer to bank / SWIFT / FEDWIRE);`beneficiaryIdentity` 加密、类型与币种金额正确传递;订单落入 `t_fundout_account_order`。
- 出款单状态流转与回调一致性、资金按指定网络与币种正确出款(详见 [[scn_online_business_merchant_payout]])。
