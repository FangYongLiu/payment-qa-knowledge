---
title: PayBy收单交易接口总览
domain: payby-acquire-transaction
kind: wiki_page
slug: payby-acquire-transaction-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:1d3b3713-3d92-4fd2-a760-42f5f4e3a4b6
tags: []
---

# PayBy收单交易接口总览

本页介绍 PayBy 收单交易接口文档的阅读对象与版本演进，帮助接入方快速了解文档定位与历史变更。相关业务域参见 [[domain_payby_acquire_transaction]]。

## 阅读对象

本文档面向接入 PayBy 的商户系统（在线购物平台、人工收银系统、自动化智能收银系统或其他）相关角色：

- 技术架构师
- 研发工程师
- 测试工程师
- 系统运维工程师

## 文档定位

本文档定义 PayBy 收单交易相关接口的协议、参数、数据模型与支付场景，覆盖创建订单、查询、退款、取消、冲正、对账、转账、卡管理、会员余额查询等能力。配套阅读：

- [[payby-acquire-payment-scenarios]]：支付场景与术语说明
- [[payby-acquire-protocol-rules]]：协议规则与请求参数规定
- [[payby-acquire-payscene-params]]：交易场景代码与 paySceneParams、interactionParams 关系
- [[payby-acquire-data-models]]：AcquireOrder、PaymentInfo、CardInfo、Money 等数据模型

## 版本演进历史

### 2.0.x 系列（基础能力构建，2020）

- **v2.0.0**（2020-02-09）初稿
- **v2.0.1** 修改申请状态；修改查询退款订单返回参数；补充接口共同参数；`paySceneParams` 改为非必填
- **v2.0.2** 补充支付场景；补充请求和响应样例；新增下载对账单接口
- **v2.0.3** 优化支付网页支付场景描述
- **v2.0.4** 修改字段名称（订单金额、净值金额）；补充返回码；修改对账文件格式；修改下载对账文件接口 URL
- **v2.0.5** `subject` 字段长度调整为 200；修改 JSAPI 调用样例代码；修改对账文件名；新增交易场景参数关系；新增每个接口的返回码归类；新增请求参数规定；新增返回码
- **v2.0.6** 修改私钥产生建议示例代码；新增产品名称示例说明；修改对账单格式与下载方式；新增单笔付款到账户/到银行卡及其查询接口；新增商户付款成功通知；商户订单号、退款商户订单号长度调整（64/32 位）
- **v2.0.7** 新增支持对公转账
- **v2.0.8** 调整返回码总览；新增 API 对应返回码；新增 InApp 支付场景；新增 `AcquireOrder.failDes`、`RefundOrder.failDes`
- **v2.0.9** 新增退款订单状态 `REFUNDED_SETTLED`
- **v2.0.10** 新增/更新下载资金对账单接口；调整查询订单/查询退款订单请求参数；新增返回码 62035
- **v2.0.11** 创建订单新增 `secondaryMerchantId`、`deviceId`；AcquireOrder/RefundOrder 同步新增；新增返回码 62036、62037、62038；查询、取消、退款订单参数补充（`orderNo`、`originOrderNo`、`originMerchantOrderNo` 等）
- **v2.0.12** 新增 `TransferOrder.failDes`、`TransferToBankOrder.failDes`
- **v2.0.13** 请求参数结构调整
- **v2.0.14** 单笔出款到账户 `beneficiaryIdentityType` 新增支持的账户类型
- **v2.0.15** 取消订单新增返回码 62001；退款订单删除返回码 62001；调整返回码 62001 原因描述
- **v2.0.16** 新增冲正接口；查询订单接口增加冲正应用场景描述；新增支付场景；创建订单新增返回码 62042；退款订单新增返回码 62040；`AcquireOrder` 新增字段 `revoked`
- **v2.0.17** 新增支付场景 `CASHTOPUP`；创建订单新增返回码 62043、62044；退款新增 62045；冲正新增 62046
- **v2.0.18** 创建订单/退款订单新增请求与返回字段 `reserved`
- **v2.0.19** 删除下载资金对账单接口；更新下载对账单接口

### 2.x 大版本（场景与能力扩展，2021–2024）

- **v2.1**（2021-03-26）新增支付场景 `FACE`；新增返回码 62047、62048
- **v2.2**（2021-05-07）新增支付场景 `DIRECTPAY`；新增返回码 62049–62065；创建订单返回新增 `PaymentInfo.cardInfo`
- **v2.3**（2021-07-14）转账接口新增 `beneficiaryAddress`
- **v2.4**（2021-08-30）新增场景参数 `oneTimePayment`；新增返回码 62073；`expiredTime` 延长至 48 小时；调整 62009 报错原因；调整退款订单应用场景描述
- **v2.5**（2022-03-30）新增返回码 62078；新增查询卡信息、解绑卡接口
- **v2.6**（2022-04-26）新增支付场景 `EWALLET`；新增返回码 62080、62081
- **v2.7**（2022-06-06）新增查询收银台 URL 信息接口；DIRECTPAY 场景 `email` 调整为可填
- **v2.8**（2022-07-01）`PAYPAGE` 新增参数 `customerId`；`cardInfo` 新增 `cardTokenExpTime`；通知类接口返回参数调整
- **v2.9**（2022-07-27）创建订单新增 `sharingParamList`、`sharingInfoList`；新增返回码 62083
- **v2.10**（2022-11-15）退款订单新增 `sharingParamList`、`refundSharingAmount`、`sharingInfoList`、`feeRefunded`；`RefundSummary` 新增 `sharingRemainRefundInfoList`；新增返回码 62083、62084
- **v2.11**（2022-12-06）新增支付场景 `PAYANDSIGN`；新增返回码 62085
- **v2.12**（2022-12-16）创建订单新增 `withholdAndRemitFee`；分账新增 `sharingSettledFeeAmount`、`withholdAndRemitFee`
- **v2.13**（2023-02-03）退款订单新增 `withholdAndRemitFee`
- **v2.14**（2023-03-22）新增更新订单超时时间接口；DIRECTPAY 新增分期场景参数；新增返回码 62087、62088
- **v2.15**（2023-07-06）创建订单新增请求/返回参数 `promotionInfoList`
- **v2.16**（2023-12-18）PAYANDSIGN 新增场景参数 `customerId`
- **v2.17**（2024-02-21）新增查询会员余额接口；`cardInfo` 新增 `issueCountry`、`issueBank`；`PaymentInfo` 新增 `channelParam`
- **v2.18**（2024-03-04）新增 `eWalletCode` 枚举
- **v2.19**（2024-06-27）创建订单请求新增 `subjectAr`
