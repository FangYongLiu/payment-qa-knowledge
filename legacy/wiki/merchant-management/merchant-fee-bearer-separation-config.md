---
title: 收支分离商户配置指南
domain: merchant-management
kind: wiki_page
slug: merchant-fee-bearer-separation-config
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:52e73b6f-0dc5-43c1-87a4-ab6d4055c18e
tags: []
---

# 收支分离商户配置指南

在 Basis 系统中通过 `Merchant Setting` 配置独立商户 MID，使其在充值、出款等场景下承担手续费扣款。

## 适用场景

- 允许指定单独的商户 MID 在充值、出款场景中承担手续费
- 由该指定商户账户扣除手续费，实现收支分离

## 配置步骤

在 Basis 系统中添加一条 `Merchant Setting` 记录，填写以下参数：

- **MerchantId**：交易发起方 MID，例如 `200000430641`
- **ParamKey**：产品码规则为 `fee_bearer_${bizProductCode}`，例如 `fee_bearer_230502`
- **ParamValue**：扣手续费的商户，规则为 `${MerchantId}|${AccountType}`，例如 `200000431881|BASIC`

## 审核流程

配置提交后需走审核流程，审核通过后配置才会生效。

## 数据存储

- 配置落库表：`acs.t_merchant_setting`

## 相关参考

- 需求单：PAYM-1068
