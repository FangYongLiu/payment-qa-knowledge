---
title: PayBy 接口返回码总览
domain: merchant-portal
kind: wiki_page
slug: payby-api-return-codes
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p18
tags: []
---

# PayBy 接口返回码总览

本页汇总 PayBy 商户接口的全部返回码（`code` / `msg`），并给出常见原因与解决方案，便于对接联调与故障定位。

## 通用返回码（成功 / 系统级）

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 0 | SUCCESS | 成功 | — |
| 400 | INVALID_PARAMETER | 参数错误 | 调整请求参数 |
| 400 | REQUESTTIME_TOO_EARLY | 请求时间比当前时间早太多 | 调整请求时间 |
| 400 | REQUESTTIME_TOO_LATER | 请求时间比当前时间晚太多 | 调整请求时间 |
| 402 | RATE_LIMIT_REJECT | 请求过于频繁 | 降低请求频率 |
| 403 | UNAUTHORIZED | API 未授权 | 联系 PayBy |
| 404 | SERVICE_NOT_AVAILABLE | API 服务不可用 | 联系 PayBy |
| 500 | SYSTEM_ERROR | 系统错误 | 联系 PayBy，稍后重试 |
| 504 | SERVICE_TIMEOUT | 服务超时 | 稍后重试 |
| 601 | RISK_FAIL | 风控校验失败 | 请调整业务 |

## 订单与状态类（62001–62017、62028–62030、62035、62040–62041）

订单生命周期与幂等性相关错误，多数需调整商户订单号、退款金额或确认订单状态。

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 62001 | ORDER_PAID | 订单已支付成功不支持撤销 | 调整商户订单号 |
| 62002 | ORDER_FAILURE | 已失败的订单再次发起撤销；已失败的订单发起退款 | 调整商户订单号 |
| 62003 | ORDER_SETTLED | 已结算的订单再次发起撤销 | 调整商户订单号 |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在 | 调整商户订单号 |
| 62006 | REFUND_AMOUNT_EXCEEDED | 退款金额大于可退金额（可退金额 = 原订单金额 − 已退金额 − 退款中金额） | 调整退款金额 |
| 62007 | REFUND_MERCHANT_ORDER_NO_NOT_EXIST | 退款商户订单号不存在 | 修改退款商户订单号 |
| 62008 | EXPIREDTIME_LESS_THAN_REQUESTTIME | 过期时间小于请求时间 | 调整过期时间 |
| 62009 | EXPIREDTIME_TOO_LATER | 过期时间超过请求时间 2 小时 | 调整过期时间 |
| 62012 | PAYSCENECODE_ILLEGAL | 非法支付场景码 | 调整支付场景码 |
| 62015 | ORDER_NOT_PAID | 订单未支付；未支付的订单发起退款 | 调整业务 |
| 62016 | MERCHANT_ORDER_NO_EXIST | 订单号相同、不同业务参数的创建订单请求 | 调整订单号 |
| 62017 | REFUND_MERCHANT_ORDER_NO_EXIST | 发起相同订单号、不同其他业务参数的退款订单请求 | 调整退款商户订单号 |
| 62028 | ORDER_SUCCESS | 订单已成功 | 调整商户订单号 |
| 62029 | ORDER_CREATED | 订单已创建 | 调整商户订单号 |
| 62030 | ORDER_BANK_FAIL | 订单已退票 | 调整商户订单号 |
| 62035 | ORDER_NO_NOT_EXIST | PayBy 订单号的订单不存在 | 调整 PayBy 订单号 |
| 62040 | ACQUIRE_ORDER_REVOKED | 订单已冲正 | 调整商户订单号 |
| 62041 | ACQUIRE_ORDER_REFUNDED | 收单订单已退款 | 调整商户订单号 |

## 收付双方与会员类（62018–62020、62023、62027、62086）

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 62018 | PAYERMID_NOT_EXIST | 付款方账号填写错误 | 调整付款方账号 |
| 62019 | PAYEEMID_NOT_EXIST | 收款方账号填写错误 | 调整收款方账户 |
| 62020 | PAYERMID_PAYEEMID_ARE_SAME | 付款人和收款人相同 | 调整付款人或收款人 |
| 62023 | NAME_NOT_MATCH | 收款人姓名不符 | 请调整收款人姓名 |
| 62027 | BENEFICIARY_NOT_EXIST | 收款人不存在 | 调整收款人 |
| 62086 | INVALID_PAYEEMID | 无效的 payeeMid | 联系 PayBy |

## 退款 / 冲正与产品 / 商户配置（62026、62038、62045–62046、62083–62084）

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 62026 | PRODUCT_IS_NOT_APPLIED | 产品未申请 | 请申请产品 |
| 62038 | INVALID_SECONDARY_MERCHANT | 发起退款的二级商户与原收单不匹配 | 调整二级商户号 |
| 62039 | REVOKE_FAILURE | PayBy 内部错误 | 联系 PayBy |
| 62045 | REFUND_REJECTED | 退款已拒绝 | 请调整业务 |
| 62046 | REVOKE_REJECTED | 冲正已拒绝 | 请调整业务 |
| 62083 | SHARING_MEMBER_NOT_EXIST | 分账会员不存在 | 调整请求参数 |
| 62084 | REFUND_SHARING_MEMBER_MISMATCH | 退款分账会员不匹配 | 调整请求参数 |

## 对账单（62013–62014）

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 62013 | STATEMENT_NOT_EXIST | 账单不存在 | 商户没有可下载的对账单 |
| 62014 | STATEMENT_NOT_GENERATED | 账单未生成 | 10 点后再下载 |

## 设备与 App 接入（62031–62034、62036–62037）

| code | msg | 原因 | 解决方案 |
| --- | --- | --- | --- |
| 62031 | MISSING_DEVICE_ID | 缺少 deviceId | 调整请求参数 |
| 62032 | MISSING_APP_ID | 缺少 appId | 调整请求参数 |
| 62033 | MISSING_AUTHCODE | 缺少 authCode | 调整请求参数 |
| 62034 | INVALID_APP_ID | 无效的 appId | 调整
