---
title: PayBy转账到银行账户接口总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p2
tags: []
---

# PayBy转账到银行账户接口总览

PayBy 转账到银行账户能力允许商户将账户资金付款至指定收款银行账户，并提供出款前的汇率与手续费试算。本页汇总该业务域的整体说明、订单状态机及受益人字段关联规则。

## 业务能力与应用场景

- **出款试算（since v2.1）**：试算汇率并返回出款手续费，便于商户在下单前预估到账金额。详见 [[api_transfer_calculate_fundout]]。
- **单笔付款到银行卡**：将账户中的资金付款到指定的收款银行账户。详见 [[api_transfer_place_to_bank_order]]。

## 订单状态机

单笔付款到银行卡订单的状态流转：

| Status | 说明 |
| --- | --- |
| CREATED | 已创建 |
| SUCCESS | 已成功 |
| FAILURE | 已失败 |
| BANK_FAIL | 银行退票 |

## 受益人类型与字段关联规则

下单时通过 `beneficiaryType` 决定受益人字段的填写要求，支持三种类型：`IBAN`（默认）、`BBAN`、`FED_WIRE`。

不同受益人类型下各字段的必填/可选/禁止规则：

| 字段 \ 类型 | IBAN | BBAN | FED_WIRE |
| --- | :---: | :---: | :---: |
| holderName | Required | Required | Required |
| iban | Required | Forbidden | Forbidden |
| swiftCode | Optional | Required | Forbidden |
| beneficiaryAddress | Required | Required | Required |
| accountNo | Forbidden | Required | Required |
| bankName | Optional | Optional | Optional |
| fedwireCode | Forbidden | Forbidden | Required |
| branchName | Optional | Optional | Optional |
| intermediaryBank | Optional | Optional | Optional |

### 受益人地址字段的特别说明

- `beneficiaryAddress` 加密传输。
- 当收款银行账户为个人账户时，`beneficiaryAddress` 必传；且 `holderName` 与 `beneficiaryAddress` 两个值的字符总和不能超过 140，否则可能导致转账失败。

## 加密字段

下单接口中以下字段需加密传输：`holderName`、`iban`、`beneficiaryAddress`、`accountNo`。

## 返回码

各接口的成功码、参数错误、风控、订单状态冲突等返回码统一参见 [[payby-transfer-to-bank-return-codes]]。
