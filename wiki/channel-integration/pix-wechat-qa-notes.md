---
title: 微信渠道接入Q&A与字段说明
domain: channel-integration
kind: wiki_page
slug: pix-wechat-qa-notes
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: []
---

# 微信渠道接入Q&A与字段说明

本页汇总微信MPC渠道接入过程中关键API的字段含义、行为约定及常见疑问点，覆盖支付、查询、退款、推定退款等核心场景。相关全局流程见 [[pix-wechat-mpc-integration-overview]]，API清单与场景映射见 [[pix-wechat-vendor-api-catalog]]。

## API: SCAN_CODE_FOR_PAYMENT

扫码下单接口，对应 `/pix/mpc/v1/create-trade`。关键字段含义：

- `PyerTrxTrmNo`：Payer terminal code，付款方终端编号，取值为 Device Id。
- `BizTp`：Bussiness type，业务类型，来源于 `QUERY_MERCHANT_CODE` 返回。
- `TrxDtTm`：Transaction date，交易日期；其日期必须与 `TrxId` 中的日期保持一致。
- `ClbckUrl`：Account institution callback acquirer institution URL，账户机构回调收单机构的URL（待确认）。
- `PrmtInf`：Marketing information，营销信息（待确认）。

下单端到端流程见 [[flow_pix_wechat_mpc_payment]]。

## API: NOTIFY_PAYMENT_RESULT

支付结果通知接口的行为说明：

- 该接口可能返回失败结果（Yes，会收到 failure）。
- 会通知交易关闭或失败的情形（Yes，trade close / failure 都会通过此接口通知）。

## API: QUERY_PAYMENT_ORDER_INFO

查询支付订单信息接口的字段是否必填问题待进一步确认：

- `PyerIDTp`：付款方证件类型，是否必填 — TODO。
- `PyerIDNo`：付款方证件号码，是否必填 — TODO。

## API: REFUND

退款接口为同步响应，无异步通知，但 WeChat 侧存在配套的查询/推定机制：

- 仅有同步响应，无异步退款结果通知。
- WeChat 会在 10 分钟内通过 `QUERY_REFUND_ORDER_INFO` 主动查询退款状态。
- 若超过该时间窗口仍未获得明确结果，则会触发 `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS`，假定退款成功。
- 允许退款失败（refund fail allowed = Yes）。
- 退款金额计算规则：`Refund pay amount = Refund transaction amount / Original transaction amount * Original pay amount`。

完整退款流程见 [[flow_pix_wechat_refund]]。

## API: NOTIFY_PRESUPPTIVE_REFUND_SUCCESS（推定退款成功通知）

用途与触发条件：

- 用途：当多次查询、且超过 10 分钟仍未拿到 WeChat 退款结果时，执行"推定退款"，即默认按退款成功处理。
- 推定通知默认只发送 1 次。
- 一旦推定成功，后续按退款成功状态推进。
- 钱包侧可通过次日账单获得推定的交易记录（参见 [[flow_pix_wechat_reconciliation]]）。

## 关联说明

- 渠道汇率与计费规则参考 [[pix-wechat-rate-sync]]。
- 渠道接入侧的配置项（`PyerAcctIssrId`、`PyeeAcctIssrId`、`AppId` 等）参考 [[pix-wechat-configuration]]。
