---
title: 收支分离商户配置指南
domain: merchant-business
kind: wiki_page
slug: merchant-fee-bearer-separation-config
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1082425488
tags: []
---

# 收支分离商户配置指南

本页说明在 Basis 系统中为指定商户配置独立 MID 扣手续费的方法，适用于充值与出款场景下的"收支分离"需求。

## 背景

- 允许配置单独的商户 MID，在 **充值 / 出款** 场景中指定某个商户账户用于扣取手续费
- 实现交易发起方与手续费扣款方的账户分离

## 配置步骤

### 1. 在 Basis 系统添加 Merchant Setting

在 Basis 系统中新增一条 Merchant Setting 记录，参数如下：

| 字段 | 示例值 | 含义 |
|---|---|---|
| MerchantId | `200000430641` | 指定商户 — 交易发起方 MID |
| ParamKey | `fee_bearer_230502` | 产品码规则：`fee_bearer_${bizProductCode}` |
| ParamValue | `200000431881|BASIC` | 实际扣手续费的商户，规则：`${MerchantId}|${AccountType}` |

### 2. 审核

提交后需经过审核流程，审核通过配置才生效。

## 参数规则说明

- **ParamKey**：以 `fee_bearer_` 为前缀，拼接业务产品码 `bizProductCode`
- **ParamValue**：由扣费商户 MID 与账户类型（AccountType，例如 `BASIC`）通过 `|` 拼接组成
- **MerchantId**：配置作用对象，即交易发起方商户

## 数据存储

- 表名：`acs.t_merchant_setting`

## 相关需求

- PAYM-1068
