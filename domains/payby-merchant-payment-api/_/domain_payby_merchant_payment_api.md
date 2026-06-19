---
id: domain_payby_merchant_payment_api
object_type: Domain
domain: payby-open-api
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki_attachment
source_ref: wiki_attachment:cc03b2a8-87d2-4334-bf2e-f10ac46eed2d
tags:
- payment
- merchant
- api
- payby
subdomain: null
module: null
sensitivity: normal
name: PayBy商户支付接口域
aliases: []
related_services: []
related_tables: []
related_scenarios:
- payby-payment-scenarios
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

PayBy商户支付接口域聚焦于商户系统（在线购物平台、人工收银系统、自动化智能收银系统等）与 PayBy 之间完成收单、退款、转账、对账及结果通知的接口体系。文档面向商户侧的技术架构师、研发工程师、测试工程师与系统运维工程师，覆盖从 v2.0.0（2020-02-09）到 v2.26（2026-01-06）的演进。

## 覆盖范围

本域涵盖 PayBy 对商户开放的全部支付相关 API 与协议规范，主要包括：

- **收单（Acquire）**：创建订单、查询订单、取消订单、冲正、更新订单超时时间
- **退款（Refund）**：退款订单、查询退款订单
- **转账/付款**：单笔付款到账户（含对公转账）、单笔付款到银行卡，及对应的查询接口
- **对账**：下载对账单接口（早期含资金对账单接口，v2.0.19 起删除）
- **卡管理**：查询卡信息（getSaveCard）、解绑卡（removeSaveCard）
- **收银台 / 会员**：查询收银台 URL 信息接口（getCashierUrlInfo）、查询会员余额接口（getMemberBalance）
- **商户通知**：支付结果通知、退款结果通知、商户付款到账户成功通知、商户付款到银行卡成功通知、拒付通知、VAM 充值通知
- **支付场景**：JSAPI、App、支付网页（PAYPAGE）、付款码、动态码、协议授权、现金充值（CASHTOPUP）、InApp、AD 广告、FACE、DIRECTPAY（含 DevicePay）、EWALLET、PAYANDSIGN、微信小程序支付、预授权（PREAUTH）等
- **公共规范**：请求参数规定、签名（私钥产生建议）、返回码体系、共同参数、对账文件格式与命名

## 关键服务/流程

- **创建订单（PlaceAcquireOrder）**：核心收单入口，支持 secondaryMerchantId、deviceId、reserved、sharingParamList、withholdAndRemitFee、promotionInfoList、subjectAr 等扩展字段；产品/商品标题（subject）长度 200，商户订单号长度 32/64。
- **退款（PlaceRefundOrder）**：支持 originOrderNo / originMerchantOrderNo、reserved、sharingParamList、refundSharingAmount、withholdAndRemitFee；返回 feeRefunded、sharingInfoList 等。
- **冲正（Revoke，v2.0.16）**：与查询订单中冲正应用场景描述配套使用。
- **更新订单超时时间（updateExpiredTime，v2.14）**：expiredTime 已延长至 48 小时（v2.4）。
- **转账接口**：PlaceTransferToBankOrderRequest 含 beneficiaryAddress、beneficiaryIdentityType；TransferOrder/TransferToBankOrder 含 failDes。
- **结果通知**：支付/退款/付款成功/拒付/VAM 充值等异步通知；v2.25 起查询与通知返回 Auth Code、RRN、Stan、Acquire Code、Acquire Message。
- **对账单**：文件名称与格式经多次调整，v2.0.19 起仅保留下载对账单接口。

## QA 关注点

- **版本兼容性**：字段、返回码与参数在多个版本中迭代（如 62001 在取消/退款语义变化、62009 报错原因调整、62035–62088 大量新增），回归测试需按版本矩阵覆盖。
- **字段长度与命名**：商户订单号 32 位 / 退款商户订单号 64 位、subject 200 字符、subjectAr（v2.19）、字段名变更（订单金额/净值金额，v2.0.4）需要校验。
- **支付场景参数**：paySceneParams 在不同场景下必填性不同（v2.0.1 调整为非必填）、oneTimePayment（v2.4）、PAYPAGE.customerId（v2.8）、PAYANDSIGN.customerId（v2.16）、DIRECTPAY 分期参数（v2.14）、DIRECTPAY email 改可填（v2.7）、DIRECTPAY 支持 DevicePay（v2.24）、agreementInfo（v2.26）。
- **状态机**：订单状态、退款订单状态（含 REFUNDED_SETTLED，v2.0.9）、revoked（v2.0.16）需覆盖正常与异常路径。
- **失败描述字段**：AcquireOrder.failDes、RefundOrder.failDes、TransferOrder.failDes、TransferToBankOrder.failDes 在异常用例中应被断言。
- **分账与代扣代缴**：sharingParamList、sharingInfoList、sharingSettledFeeAmount、withholdAndRemitFee、sharingRemainRefundInfoList、refundSharingAmount 的金额一致性。
- **卡信息扩展**：cardInfo.issueCountry、cardInfo.issueBank（v2.17）、cardTokenExpTime（v2.8）、PaymentInfo.cardinfo（v2.2）、PaymentInfo.channelParam（v2.17）。
- **通知签名与重放**：各类通知（含拒付、VAM 充值）参数调整后需校验签名、幂等与重试。
- **对账文件**：文件名/格式历次调整需在自动化对账脚本中同步。
- **返回码归类**：v2.0.5 起每个接口都有返回码归类，QA 应按接口维度建立返回码用例库。

详见 [[payby-merchant-api-overview]] 与 [[payby-payment-scenarios]]。
