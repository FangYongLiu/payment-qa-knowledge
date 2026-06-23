---
title: PayBy支付场景现状梳理(DirectPay/PayAndSign/AutoDebit)
domain: payby-authorization-protocol
kind: wiki_page
slug: payment-scenarios-overview
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/702709784
tags: []
---

# PayBy支付场景现状梳理(DirectPay/PayAndSign/AutoDebit)

本页梳理 PayBy 当前三种核心支付场景（DirectPay、PayAndSign、AutoDebit）的定义、卡状态语义、系统交互现状以及目前已知的 3DS 降级导致 CardToken 无法代扣问题。

## 支付场景定义

- **Direct Pay**：直连支付。用户完成支付时，卡信息被 PayBy 存储，返回 `CardToken`，后续可凭 `CardToken` 继续支付。
- **PAYANDSIGN**：支付并签约代扣协议。用户完成支付即视为认可代扣协议，PayBy 生成并生效代扣协议。
- **AUTODEBIT**：授权支付。用户使用已生效的代扣协议完成支付。

> 产品与支付场景对应关系参考：`01-Product Matrix`

## 卡状态定义

- **激活**：已激活的卡可以用卡 id 查询出卡信息。
- **认证**：用于风控判断风险；未认证卡可走 3DS 认证（认证时需提供 cvv）。

## 系统交互现状

### Direct Pay
- **首次支付**：用户使用卡完成支付，支付成功后 `CardToken` 通过 notify 方式回传给商户。
- **使用已有卡支付**：商户后续可使用已返回的 `CardToken` 直接发起支付。

详见 [[scn_directpay_first_and_subsequent]]。

### PAYANDSIGN
- 用户完成支付时，代扣协议生效，协议号通过通知方式回传给商户。
- 后续商户可使用协议号发起代扣。

详见 [[scn_payandsign_payment]]。

### AUTODEBIT
- 商户使用已生效的代扣协议号直接发起支付。

详见 [[scn_autodebit_payment]]。

## 当前已知问题：3DS 降级导致 CardToken 代扣失败

**问题描述**：
- Direct Pay 第一次支付成功后返回卡 token 给商户，但商户下次使用卡 token 代扣失败。
- 原因：首次 3DS 支付被降级；当前策略下，3DS 降级后不会更新卡为「激活」状态，卡未激活则无法代扣。

**解决方案（讨论中）**：
1. 支付成功 → 更新卡状态为「激活」。
2. 支付成功且非 3DS 降级 → 更新卡认证状态为「已认证」。
3. 特约商户 motoPay 包装新接口，独立给特约商户授权，不绑卡，直接 moto 扣款。

排查与处理细节见 [[ts_directpay_3ds_downgrade_token_invalid]]。
