---
title: PayBy单笔付款到银行卡接口总览
domain: fund-out-transfer
kind: wiki_page
slug: payby-openapi-transfer-to-bank
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p14
tags: []
---

# PayBy单笔付款到银行卡接口总览

PayBy 单笔付款到银行卡（Transfer To Bank）允许商户将账户余额付款到指定的收款银行账户，并提供下单与查询两个核心接口。

## 应用场景

- 商户将自身 PayBy 账户中的资金，付款到指定的收款银行账户（IBAN）。
- 支持按商户订单号查询付款的最终结果。

## 订单状态机

| Status | 说明 |
| --- | --- |
| CREATED | 已创建 |
| SUCCESS | 已成功 |
| FAILURE | 已失败 |
| BANK_FAIL | 银行退票 |

## 相关接口

本业务域包含两个接口：

- [[api_payby_place_transfer_to_bank_order]]：创建单笔付款到银行卡订单（`/sgs/api/transfer/placeTransferToBankOrder`），下单后订单初始状态为 `CREATED`。
- [[api_payby_get_transfer_to_bank_order]]：根据 `merchantOrderNo` 查询单笔付款到银行卡订单的详细结果（`/sgs/api/transfer/getTransferToBankOrder`）。

## 关键业务对象

两个接口的响应体均通过 `TransferToBankOrder` 返回订单信息，常见字段包括：

- `merchantOrderNo`：商户订单号
- `orderNo`：PayBy 订单号
- `amount`：金额（`Money` 类型，含 `amount`/`currency`）
- `holderName`、`iban`、`beneficiaryAddress`：收款人信息（加密传输/响应中以密文返回）
- `swiftCode`：收款银行 SwiftCode
- `memo`：付款备注
- `notifyUrl`：商户接收通知的地址
- `product`：固定为 `Transfer To Bank`
- `status`：订单状态（见上文状态机）
- `requestTime`：请求时间
- `paymentInfo`（仅查询响应）：含 `arrivalTime`、`payerFeeAmount` 等

## 收款人地址注意事项

- 若收款银行账户为个人账户，必须传 `beneficiaryAddress`。
- `holderName` 与 `beneficiaryAddress` 字符总长度不得超过 140，否则可能导致付款失败。

## 公共请求约定

- Http Header 必填：`sign`、`Partner-Id`；可选 `Content-Language`（如 `en`）。
- Http Body 必填：`requestTime`（Timestamp(3)）和 `bizContent`（业务内容）。
- 详细请求/响应字段、签名样例与返回码请见各接口子页。
