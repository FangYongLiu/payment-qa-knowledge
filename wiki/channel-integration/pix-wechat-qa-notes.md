---
title: PIX微信接入Q&A与字段说明
domain: channel-integration
kind: wiki_page
slug: pix-wechat-qa-notes
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags: []
---

# PIX微信接入Q&A与字段说明

本页汇总 PIX 微信 MPC 渠道接入过程中各 Vendor API 的字段含义、行为约定与常见问答，便于联调与异常排查。相关流程见 [[pix-wechat-system-flow]]，API 清单见 [[pix-wechat-vendor-api-catalog]]。

## API: SCAN_CODE_FOR_PAYMENT

用于扫码后向微信侧创建交易单，相关业务流程见 [[flow_pix_wechat_mpc_payment]]。

字段含义说明：

- `PyerTrxTrmNo`：Payer terminal code，即 Device Id（付款方终端编号）。
- `BizTp`：Bussiness type，业务类型，取自 `QUERY_MERCHANT_CODE` 的返回结果。
- `TrxDtTm`：交易日期时间，需保证 `TrxDtTm` 的日期与 `TrxId` 中的日期一致。
- `ClbckUrl`：Account institution callback acquirer institution URL，账户机构回调收单机构的 URL。
- `PrmtInf`：Marketing information，营销信息。

## API: NOTIFY_PAYMENT_RESULT

- 该接口是否可能收到失败结果？**会**，存在失败回调的可能。
- 是否会通知交易关闭或失败？**会**，关闭与失败场景均会通过该接口通知。

## API: QUERY_PAYMENT_ORDER_INFO

字段是否必填的疑问：

- `PyerIDTp`：是否必填待确认（TODO）。
- `PyerIDNo`：是否必填待确认（TODO）。

## API: REFUND

退款流程详见 [[flow_pix_wechat_refund]]。

- 是否仅有同步响应、没有异步通知？**没有异步响应**。微信会在 10 分钟内通过 `QUERY_REFUND_ORDER_INFO` 主动查询退款结果。
- 超过该 10 分钟窗口仍无结果时，会触发 `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS`（退款推定成功）。
- 退款是否允许失败？**允许**。

## API: NOTIFY_PRESUPPTIVE_REFUND_SUCCESS

- 用途：见 `REFUND` 中关于退款推定的说明。
- 触发条件：实际上已经经过多次查询且长时间（约 10 分钟）仍无结果时才会执行推定。
- 通知次数：默认只会推定通知 **1 次**。
- 处理原则：一旦推定，按 **退款成功** 处理。
- 后续核对：钱包侧可通过次日账单获得推定的交易记录，对账逻辑见 [[flow_pix_wechat_reconciliation]]。
