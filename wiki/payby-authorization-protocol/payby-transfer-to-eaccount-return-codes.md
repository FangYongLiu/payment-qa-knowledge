---
title: PayBy转账到电子账户接口返回码总览
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-transfer-to-eaccount-return-codes
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-transfer-v1.1-p2
tags: []
---

# PayBy转账到电子账户接口返回码总览

本页汇总 PayBy 转账到电子账户接口的通用返回码以及订单错误原因代码，便于在联调与线上排障时快速定位问题与确定处理方式。

## 通用返回码

| code  | msg                         | 原因                                             | 解决方案               |
| ----- | --------------------------- | ------------------------------------------------ | ---------------------- |
| 0     | SUCCESS                     | 成功                                             |                        |
| 400   | INVALID_PARAMETER           | 参数错误                                         | 调整请求参数           |
| 400   | REQUESTTIME_TOO_EARLY       | 请求时间比当前时间早太多                         | 调整请求时间           |
| 400   | REQUESTTIME_TOO_LATER       | 请求时间比当前时间晚太多                         | 调整请求时间           |
| 402   | RATE_LIMIT_REJECT           | 请求过于频繁                                     | 降低请求频率           |
| 403   | UNAUTHORIZED                | API未授权                                        | 联系PayBy              |
| 404   | SERVICE_NOT_AVAILABLE       | API服务不可用                                    | 联系PayBy              |
| 500   | SYSTEM_ERROR                | 系统错误                                         | 联系PayBy,稍后重试     |
| 504   | SERVICE_TIMEOUT             | 服务超时                                         | 稍后重试               |
| 601   | RISK_FAIL                   | 风控校验失败                                     | 请调整业务             |
| 62002 | ORDER_FAILURE               | 已失败的订单再次发起撤销；已失败的订单发起退款   | 调整商户订单号         |
| 62004 | MERCHANT_ORDER_NO_NOT_EXIST | 商户订单号的订单不存在                           | 调整商户订单号         |
| 62016 | MERCHANT_ORDER_NO_EXIST     | 订单号相同,不同业务参数的创建订单请求            | 调整订单号             |
| 62020 | PAYERMID_PAYEEMID_ARE_SAME  | 付款人和收款人相同                               | 调整付款人或者收款人   |
| 62023 | NAME_NOT_MATCH              | 收款人姓名不符                                   | 请调整收款人姓名       |
| 62026 | PRODUCT_IS_NOT_APPLIED      | 产品未申请                                       | 请申请产品             |
| 62027 | BENEFICIARY_NOT_EXIST       | 收款人不存在                                     | 调整收款人             |
| 62028 | ORDER_SUCCESS               | 订单已成功                                       | 调整商户订单号         |
| 62029 | ORDER_CREATED               | 订单已创建                                       | 调整商户订单号         |

## 订单错误原因代码

用于订单失败场景下的细分原因定位，主要覆盖风控、限额与渠道侧的拒绝。

| code  | msg                                          | 原因             | 解决方案     |
| ----- | -------------------------------------------- | ---------------- | ------------ |
| 92000 | Risk control rejection                       | 风控拒绝         | 请调整业务   |
| 92001 | The amount of transaction exceeds the limit  | 交易金额超限     | 请调整业务   |
| 92002 | The number of transactions exceeds the limit | 交易次数超限     | 请调整业务   |
| 92003 | Non KYC user transactions                    | 用户未完成 kyc   | 请调整业务   |
| 92004 | Channel rejection                            | 渠道拒绝         | 请调整业务   |

## 排障建议

- **参数与时间类**（`400`）：先核对请求参数与请求时间戳，确保时间在允许偏差范围内。
- **频率与可用性类**（`402`/`404`/`504`）：降低请求频率或稍后重试；持续不可用时联系 PayBy。
- **授权与系统类**（`403`/`500`）：`UNAUTHORIZED` 需联系 PayBy 确认 API 授权；`SYSTEM_ERROR` 可稍后重试。
- **风控类**（`601`、`92000`～`92004`）：需根据具体子码调整业务，如金额、频次、KYC 状态、渠道选择等。
- **订单状态类**（`62002`/`62004`/`62016`/`62028`/`62029`）：均与商户订单号语义冲突有关，应调整商户订单号后重试。
- **业务关系类**（`62020`/`62023`/`62026`/`62027`）：核对付款人/收款人信息及产品申请状态。
