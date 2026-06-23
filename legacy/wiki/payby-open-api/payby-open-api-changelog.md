---
title: PayBy 开放接口版本变更历史
domain: payby-open-api
kind: wiki_page
slug: payby-open-api-changelog
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
source_type: upload
source_ref: api-docs/payby-api-v2.25-p2
tags: []
---

# PayBy 开放接口版本变更历史

本页按版本顺序记录 PayBy 开放接口文档（参见 [[payby-open-api-overview]]）从 v2.0.0 起每次发布的修改点。

## 早期版本（v2.0.0 – v2.0.9）

- **v2.0.0（2020-02-09）**：初稿。
- **v2.0.1（2020-02-09）**：修改申请状态；修改查询退款订单返回参数；补充接口共同参数；创建订单接口参数 `paySceneParams` 调整为非必填。
- **v2.0.2（2020-02-10）**：补充支付场景；补充请求和响应样例；新增下载对账单接口。
- **v2.0.3（2020-02-12）**：优化支付网页支付场景描述。
- **v2.0.4（2020-02-14）**：修改字段名称（订单金额、净值金额）；补充返回码；修改对账文件格式；修改下载对账文件接口 URL。
- **v2.0.5（2020-02-20）**：商品标题 `subject` 字段长度调整为 200；修改 JSAPI 调用样例；修改对账文件名称；新增交易场景参数关系中的参数和说明；为每个接口新增返回码归类；新增请求参数规定与新返回码。
- **v2.0.6（2020-02-23）**：修改私钥生成示例代码；新增产品名称示例；修改对账单格式与下载方式；新增"单笔付款到账户"接口及其查询接口；新增"单笔付款到银行卡"接口及其查询接口；新增商户付款成功通知；商户订单号、退款商户订单号长度调整为 64 位；商户订单号长度调整为 32 位。
- **v2.0.7（2020-03-31）**：新增支持对公转账。
- **v2.0.8（2020-05-08）**：调整返回码总览；新增 API 对应返回码；新增 InApp 支付场景；新增字段 `AcquireOrder.failDes`、`RefundOrder.failDes`。
- **v2.0.9（2020-05-03）**：新增退款订单状态 `REFUNDED_SETTLED`。

## 对账与字段补充（v2.0.10 – v2.0.15）

- **v2.0.10（2020-06-10）**：新增"下载资金对账单"接口；更新下载对账单接口；调整查询订单、查询退款订单的请求参数；新增返回码 `62035`。
- **v2.0.11（2020-06-16）**：创建订单新增请求参数 `secondaryMerchantId`、`deviceId`；`AcquireOrder` 新增同名字段；新增返回码 `62036`、`62037`；`RefundOrder` 新增 `secondaryMerchantId`、`deviceId`；退款订单新增同名请求参数；新增返回码 `62038`；查询订单/查询退款订单的 `merchantOrderNo`、`refundMerchantOrderNo` 新增描述；取消订单新增请求参数 `orderNo`，`merchantOrderNo` 新增描述；退款订单新增请求参数 `originOrderNo`，`originMerchantOrderNo` 新增描述。
- **v2.0.12（2020-06-24）**：新增字段 `TransferOrder.failDes`、`TransferToBankOrder.failDes`。
- **v2.0.13（2020-06-29）**：请求参数结构调整。
- **v2.0.14（2020-07-03）**：单笔出款到账户的 `beneficiaryIdentityType` 新增支持的账户类型。
- **v2.0.15（2020-08-13）**：取消订单新增返回码 `62001`；退款订单删除返回码 `62001`；调整 `62001` 原因描述。

## 冲正与新支付场景（v2.0.16 – v2.0.19）

- **v2.0.16（2020-08-14）**：新增冲正接口；查询订单接口增加冲正应用场景描述；新增支付场景；创建订单新增返回码 `62042`；退款订单新增返回码 `62040`；`AcquireOrder` 新增字段 `revoked`。
- **v2.0.17（2020-10-26）**：新增支付场景 `CASHTOPUP`；创建订单新增返回码 `62043`、`62044`；退款新增返回码 `62045`；冲正新增返回码 `62046`。
- **v2.0.18（2020-12-22）**：创建订单与退款订单分别新增请求字段 `reserved` 与返回字段 `reserved`。
- **v2.0.19（2021-01-13）**：删除"下载资金对账单"接口；更新下载对账单接口。

## 卡支付与卡管理（v2.1 – v2.5）

- **v2.1（2021-03-26）**：新增支付场景 `FACE`；创建订单新增返回码 `62047`、`62048`。
- **v2.2（2021-05-07）**：新增支付场景 `DIRECTPAY`；创建订单新增返回码 `62049`–`62065`；创建订单返回新增字段 `PaymentInfo.cardinfo`。
- **v2.3（2021-07-14）**：新增字段 `PlaceTransferToBankOrderRequest.beneficiaryAddress` 和 `TransferToBankOrder.beneficiaryAddress`。
- **v2.4（2021-08-30）**：新增支付场景参数 `oneTimePayment`；创建订单新增返回码 `62073`；创建订单请求参数 `expiredTime` 延长至 48 小时；调整返回码 `62009` 报错原因；调整退款订单应用场景描述。
- **v2.5（2022-03-30）**：创建订单新增返回码 `62078`；新增查询卡信息接口；新增解绑卡接口。

## 钱包、收银台与通知（v2.6 – v2.8）

- **v2.6（2022-04-26）**：新增支付场景 `EWALLET`；创建订单新增返回码 `62080`、`62081`。
- **v2.7（2022-06-06）**：新增查询收银台 URL 信息接口；`DIRECTPAY` 场景参数 `email` 调整为可填。
- **v2.8（2022-07-01）**：支付场景 `PAYPAGE` 新增参数 `customerId`；`cardInfo` 新增返回字段 `cardTokenExpTime`；调整支付结果通知、退款结果通知、商户付款到账户成功通知、商户付款到银行卡成功通知的返回参数。

## 分账能力（v2.9 – v2.13）

- **v2.9（2022-07-27）**：创建订单新增请求参数 `sharingParamList`、新增返回参数 `sharingInfoList`；新增返回码 `62083`。
- **v2.10（2022-11-15）**：退款订单新增请求参数 `sharingParamList`、`refundSharingAmount`；新增返回码 `62083`、`62084`；新增返回参数 `sharingInfoList`、`feeRefunded`；`RefundSummary` 新增返回参数 `sharingRemainRefundInfoList`。
- **v2.11（2022-12-06）**：新增支付场景 `PAYANDSIGN`；创建订单新增返回码 `62085`。
- **v2.12（2022-12-16）**：创建订单新增请求参数 `withholdAndRemitFee`；分账新增返回参数 `sharingS
