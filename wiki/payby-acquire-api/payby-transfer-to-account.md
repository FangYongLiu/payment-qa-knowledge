---
title: PayBy单笔付款到账户
domain: payby-open-api
kind: wiki_page
slug: payby-transfer-to-account
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p13
tags: []
---

# PayBy单笔付款到账户

企业付款到用户账户业务，支持向个人手机号或企业会员ID发起单笔转账，并通过查询接口获取付款最终结果。属于 [[payby-acquire-api-overview]] 的子能力。

## 业务场景

- **下单**：企业付款为企业提供付款到用户账户的能力。详见 [[api_payby_transfer_place_order]]。
- **查询**：用于单笔付款到账户的结果查询，返回付款的详细结果。详见 [[api_payby_transfer_get_order]]。

## 状态机

订单状态枚举：

| Status | 说明 |
| ------ | ---- |
| CREATED | 已创建 |
| SUCCESS | 已成功 |
| FAILURE | 已失败 |

## 关键参数

下单核心参数（PlaceTransferOrderRequest）：

- `merchantOrderNo`：商户订单号，String(64)，必填
- `beneficiaryIdentityType`：用户标识类型，必填，枚举值：
  - `PHONE_NO`：手机号（个人收款方使用）
  - `MEMBER_ID`：会员ID（企业收款方使用）
- `beneficiaryIdentity`：用户标识，必填，加密传输
  - 标识类型为手机号时填带区号的手机号（示例：`971-585812345`）
  - 标识类型为会员ID时填会员ID
- `beneficiaryFullName`：收款用户姓名，可选，String(100)，加密传输；上传则强制校验姓名
- `amount`：金额（Money 类型），必填
- `memo`：企业付款备注，必填，String(128)
- `notifyUrl`：后端通知地址，可选

查询核心参数（GetTransferOrderRequest）：

- `merchantOrderNo`：商户订单号，必填

## 响应订单信息

下单和查询响应均返回 `transferOrder`（TransferOrder 对象），包含字段：

- `orderNo`：PayBy订单号
- `merchantOrderNo`：商户订单号
- `beneficiaryIdentityType` / `beneficiaryIdentity` / `beneficiaryFullName`：收款方信息（加密返回）
- `amount`：付款金额
- `memo`：付款备注
- `notifyUrl`：通知地址
- `product`：产品名（`Transfer`）
- `requestTime`：请求时间
- `status`：订单状态（CREATED/SUCCESS/FAILURE）
- `paymentInfo`：付款信息
  - `arrivalTime`：到账时间
  - `payerFeeAmount`：付款方手续费

## 接口地址

**下单（placeTransferOrder）**

- 联调：`https://uat.test2pay.com/sgs/api/transfer/placeTransferOrder`
- 生产：`https://api.payby.com/sgs/api/transfer/placeTransferOrder`

**查询（getTransferOrder）**

- 联调：`https://uat.test2pay.com/sgs/api/transfer/getTransferOrder`
- 生产：`https://api.payby.com/sgs/api/transfer/getTransferOrder`

## 通用约束

- Http Header 必填 `Sign`、`Partner-Id`，可选 `Content-Language`
- Http Body 必填 `requestTime`（Timestamp(3)）、`bizContent`
- 响应 Body 中的 `body` 字段仅在 `applyStatus=SUCCESS` 且 `code=0` 时返回

## 业务返回码（特有）

下单接口（placeTransferOrder）特有错误码：

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 62002 | ORDER_FAILURE | 订单已失败 | 调整商户订单号 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同，不同业务参数的创建订单请求 | 调整订单号 |
| 62020 | PAYERMID_PAYEEMID_ARE_SAME | 付款人和收款人相同 | 调整付款人或收款人 |
| 62023 | NAME_NOT_MATCH | 收款人姓名不符 | 调整收款人姓名 |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 | 申请产品 |
| 62027 | BENEFICIARY_NOT_EXIST | 收款人不存在 | 调整收款人 |
| 62028 | ORDER_SUCCESS | 订单已成功 | 调整商户订单号 |
| 62029 | ORDER_CREATED | 订单已创建 | 调整商户订单号 |

查询接口（getTransferOrder）特有错误码：

| code | msg | 原因 | 解决方案 |
| ---- | --- | ---- | -------- |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |

通用错误码（如 `INVALID_PARAMETER`、`REQUESTTIME_TOO_EARLY/LATER`、`RATE_LIMIT_REJECT`、`UNAUTHORIZED`、`SERVICE_NOT_AVAILABLE`、`SYSTEM_ERROR`、`SERVICE_TIMEOUT`、`RISK_FAIL`）参见 [[payby-acquire-api-overview]] 与具体接口页。
