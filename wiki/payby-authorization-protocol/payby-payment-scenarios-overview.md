---
title: PayBy支付场景现状梳理(DirectPay/PayAndSign/AutoDebit)
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-payment-scenarios-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:70f3c536-29f9-4b13-84f9-fdd88653b2d6
tags: []
---

# PayBy支付场景现状梳理(DirectPay/PayAndSign/AutoDebit)

本页梳理 PayBy 当前三种支付场景（Direct Pay、PAYANDSIGN、AUTODEBIT）的定义、卡状态语义、系统交互流程，以及 3DS 降级导致后续代扣失败的现状问题与方案讨论。

## 支付场景定义

- **Direct Pay**：直连支付。用户完成支付时卡信息被 PayBy 存储，返回 `CardToken`，后续可凭 `CardToken` 继续支付。
- **PAYANDSIGN**：支付并签约代扣协议。用户完成支付即视为认可代扣协议，PayBy 生成代扣协议并使其生效。
- **AUTODEBIT**：授权支付。用户使用已生效的代扣协议完成支付。

> 产品与支付场景对应关系参考：`01-Product Matrix`

## 卡状态定义

- **激活**：已激活的卡可通过卡 id 查询卡信息。
- **认证**：用于风控判断风险。未认证的卡可走 3DS 认证（认证时需提供 cvv）。

## 系统交互现状

### Direct Pay

- **首次支付**：用户输入卡信息完成支付，支付成功后通过 notify 将 `CardToken` 返回给商户。
- **使用已有卡支付**：商户使用已获得的 `CardToken` 直接发起后续支付。

### PAYANDSIGN

- 用户完成首次支付，代扣协议同时生效。
- 协议号通过通知返回给用户，后续可用协议号发起代扣。

### AUTODEBIT

- 使用已生效的代扣协议号直接发起支付。

## 当前出现的问题

**问题描述**

- Direct Pay 首次支付成功后会返回卡 token 给商户。
- 商户下次使用卡 token 发起代扣时失败。
- 根因：首次 3DS 支付被降级，当前策略下降级后不更新卡为激活状态；卡未激活则无法代扣。

## 解决方案（讨论中）

- 支付成功即更新卡状态为**激活**。
- 支付成功且**非 3DS 降级**时，更新卡的认证状态为**已认证**。
- 针对特约商户的 motoPay：包装新接口，独立给特约商户授权，不绑卡，直接 moto 扣款。
