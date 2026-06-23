---
title: PayBy 转账到银行账户接口总览
domain: fund-out-transfer
kind: wiki_page
slug: payby-transfer-to-bank-overview
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-tobank-v2.4-p3
tags: []
---

# PayBy 转账到银行账户接口总览

本页汇总 PayBy「转账到银行账户」业务域的接口清单、核心流程与异步通知机制，便于快速定位相关能力。

## 业务范围

- 业务域：`payby-transfer-to-bank`
- 产品标识：`Transfer To Bank`
- 覆盖能力：商户付款到银行卡的结果查询，以及付款结果的异步通知接收。
- 具体到账时间因各银行结算时间不同，以实际到账时间为准。

## 接口清单

| 类型 | 名称 | 说明 |
| --- | --- | --- |
| 主动查询 | [[api_payby_get_transfer_to_bank_order]] | 通过 `merchantOrderNo` 查询单笔付款到银行卡的最终结果 |
| 异步通知 | [[api_payby_transfer_to_bank_notify]] | PayBy 在付款有结果后向商户 `notifyUrl` 推送 `transferToBankOrder` 数据 |

## 环境地址

- 联调：`https://uat.test2pay.com`
- 生产：`https://api.payby.com`
- 查询接口路径：`/sgs/api/transfer/getTransferToBankOrder`

## 通用约定

- 请求/响应均由 Http Header + Http Body(JSON) 组成。
- Header 必填：`Sign`、`Partner-Id`；可选：`Content-Language`(如 `en`)。
- Body 公共字段：`requestTime`(Timestamp(3))、`bizContent`(业务内容)。
- 签名算法：通用请求与异步通知一致，通知由 PayBy RSA 私钥签名，商户使用从商户 portal 下载的 PayBy 公钥验签。

## 处理流程建议

1. 商户发起付款到银行卡（创建订单，本页不展开）。
2. PayBy 处理后，通过异步通知推送结果到商户 `notifyUrl`。
3. 商户对通知做幂等处理并返回 `SUCCESS`。
4. 若订单状态不明或未收到通知，商户应主动调用查询接口确认结果。

## 异步通知机制

- 通知格式与普通请求相同（HTTP + JSON Body）。
- 同一通知可能被重复发送，商户系统必须支持幂等处理。
- 商户响应不符合规范或超时视为失败，PayBy 会重试。
- 默认重试 7 次，间隔（分钟）：`2, 10, 10, 60, 120, 360, 900`；不保证最终一定送达。
- 商户接收成功须返回字符串 `SUCCESS`，其他视为异常。
- 通知 Body 主体字段：`transferToBankOrder`(类型 `TransferToBankOrder`)。

## 核心数据对象

`TransferToBankOrder` 主要字段（在查询响应与异步通知中复用）：

- `merchantOrderNo`：商户订单号
- `orderNo`：PayBy 订单号
- `amount`：金额（含 `amount`/`currency`）
- `holderName`、`iban`、`swiftCode`、`beneficiaryAddress`：收款方信息
- `memo`：备注
- `product`：产品名，固定为 `Transfer To Bank`
- `notifyUrl`：通知地址
- `requestTime`：请求时间
- `status`：订单状态（如 `SUCCESS`）
- `paymentInfo.arrivalTime`：到账时间
- `paymentInfo.payerFeeAmount`：付款方手续费
- `bankReference`：银行参考号（查询响应中返回）

## 返回码

完整返回码（含查询接口与转账业务通用错误码）请参见 [[payby-transfer-to-bank-return-codes]]。
