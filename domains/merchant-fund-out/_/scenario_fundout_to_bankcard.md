---
id: scn_fundout_to_bankcard
object_type: Scenario
domain: fund-out-transfer
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1012367385
tags:
- transfer
- fundout
- bankcard
subdomain: null
module: null
sensitivity: normal
name: 商户出款到卡
aliases: []
related_services: []
related_tables:
- mhtfundout.t_fundout_bankcard_order
- mhtfundout.t_fundout_bankcard_beneficiary
- mhtfundout.t_account_beneficiary_history
related_scenarios:
- scn_fundout_to_account
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
- 产品集：Transfer
- SGS 接口：`transfer/placeTransferToBankOrder`
- 接口文档：https://developers.payby.com/docs/Transfer%20to%20bank/transfer-to-bank
- 入口渠道：商户控台

## 前置条件
- 商户已开通 Transfer 产品集
- 已完成绑卡（受益人信息记录于 `member.tr_beneficiary_info`）

## 操作步骤
1. 商户在控台或通过 SGS 调用 `transfer/placeTransferToBankOrder`
2. 提交银行卡出款请求，重要参数：
   - `swiftCode`: BBMEAEAD
   - `iban`: 加密|AE470200000012213138001
   - `holderName`: 加密|CAN WANG
   - `networkCode`: LOCAL
   - `countryCode`: UAE
   - `fundoutCurrencyCode`: AED
   - `beneficiaryType`: IBAN
   - `beneficiaryAddress`: 加密|sigma 1 tower

## DB 校验点
- `mhtfundout.t_fundout_bankcard_order`：出款到卡订单
- `mhtfundout.t_fundout_bankcard_beneficiary`：出款到卡受益人信息
- `mhtfundout.t_account_beneficiary_history`：受益人历史记录

## 预期结果
- 银行卡出款订单成功落库到 `mhtfundout.t_fundout_bankcard_order`
- 受益人信息保存至 `mhtfundout.t_fundout_bankcard_beneficiary` 与 `mhtfundout.t_account_beneficiary_history`
- 资金按照 `networkCode=LOCAL` 等参数完成出款到指定银行卡
