---
title: PayBy转账到银行账户接口总览
domain: payby-transfer-to-bank
kind: wiki_page
slug: payby-transfer-to-bank-overview
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-bankcard-v0.2-p3
tags: []
---

# PayBy转账到银行账户接口总览

本页汇总 PayBy 转账到银行账户业务域下的接口集合、调用流程与通用约定，便于快速定位查询、通知与错误处理相关能力。

## 业务范围

- 用于商户向银行卡发起转账后的结果查询与异步通知处理。
- 实际到账时间因各银行结算时间而异，以最终到账时间为准。

## 接口集合

| 接口 | 用途 |
| ---- | ---- |
| [[api_payby_get_transfer_to_bank_card]] | 查询转账到银行卡订单的详细结果 |
| [[api_payby_transfer_bank_card_notify]] | 接收 PayBy 推送的转账银行卡成功通知 |

## 调用流程

1. 商户发起转账到银行卡（创建订单，由独立接口完成）。
2. PayBy 处理转账结果后，向商户 `notifyUrl` 推送 [[api_payby_transfer_bank_card_notify]]。
3. 商户接收通知并返回 `SUCCESS` 应答；若结果不明或未收到通知，主动调用 [[api_payby_get_transfer_to_bank_card]] 查询订单状态。

## 通用约定

### 协议与报文

- HTTP 协议，请求与通知均由 Http Header + Http Body（JSON）组成。
- Body 通用结构：`requestTime`（Timestamp(3)）+ `bizContent`（业务内容）。
- 响应 Body 通用结构：`head`（ResponseHeader）+ `body`（业务响应）。

### Header 字段

| 字段 | 必填 | 说明 |
| ---- | ---- | ---- |
| `Content-Language` | Optional | 文案语言，如 `en` |
| `Sign` | Required | 签名 |
| `Partner-Id` | Required | 商户号，String(12) |

### 环境地址

- 联调（UAT）：`https://uat.test2pay.com`
- 生产：`https://api.payby.com`
- 路径前缀：`/sgs/api/transfer/`

### 签名与验签

- 请求与通知均需签名，算法一致。
- 通知由 PayBy RSA 私钥签署，商户使用 Portal 下载的 PayBy 公钥进行验签。

## 异步通知规则

- 同一通知可能重复推送，商户系统必须做幂等处理。
- 商户响应不符合规范或超时视为失败，PayBy 将重试。
- 默认重试 7 次，间隔（单位：分钟）：`2, 10, 10, 60, 120, 360, 900`；不保证最终送达。
- 商户收到通知后必须返回字符串 `SUCCESS`，否则视为异常。

## 关键数据对象

- `TransferBankCardOrder`：转账银行卡订单信息，贯穿查询响应与异步通知。
- 订单状态字段：`status`（如 `CREATED`）。
- 持卡人类型：`accountHolderType`（如 `INDIVIDUAL`）。
- 卡号、姓名等敏感字段在响应中以加密形式返回。

## 错误处理

- 各接口返回码语义统一，详见 [[payby-transfer-to-bank-return-codes]]。
- 高频场景：
  - `62004 MERCHANT_ORDER_NO_NOT_EXIST`：商户订单号不存在。
  - `62016 MERCHANT_ORDER_NO_EXIST`：订单号重复但业务参数不同。
  - `62028 ORDER_SUCCESS` / `62029 ORDER_CREATED`：订单已处于对应状态。
  - `601 RISK_FAIL`：风控校验失败。
