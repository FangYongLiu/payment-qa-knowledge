---
title: PIX微信Vendor API清单与配置
domain: channel-integration
kind: wiki_page
slug: pix-wechat-vendor-api-catalog
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a68e3cf4-694f-4d32-9a67-4b4aaeee8675
tags: []
---

# PIX微信Vendor API清单与配置

本页汇总微信(Wechat) MPC 渠道对接所涉及的 Vendor API 场景映射、Requester/Responder 角色、以及 Wechat 渠道的关键配置项。整体业务场景与系统流程见 [[pix-wechat-mpc-overview]] 与 [[pix-wechat-system-flow]]。

## Vendor API 场景映射

下表列出 PIX 与微信对接的各业务场景对应的 API、调用方向（Requester=主动调用 vendor / Responder=接收 vendor 调用并响应）。

| 场景 | 入口 / 触发 | Wechat API | 角色 |
| --- | --- | --- | --- |
| 解析商户码 | `/pix/mpc/v1/parse` | `QUERY_MERCHANT_CODE` | Requester |
| 创建交易并支付 | `/pix/mpc/v1/create-trade` | `SCAN_CODE_FOR_PAYMENT` | Requester |
| 处理交易结果 | process trade result | `NOTIFY_PAYMENT_RESULT` | Requester |
| 退款 | refund | `REFUND` | Responder |
| 关闭支付 | close payment | `CLOSE_PAYMENT` | Responder |
| 查询支付 | query payment | `QUERY_PAYMENT_ORDER_INFO` | Responder |
| 查询退款 | query refund | `QUERY_REFUND_ORDER_INFO` | Responder |
| 下载对账文件 | download reconciliation file | `QUERY_BILL_ADDRESS` | Requester |
| 通知最终支付结果 | notify final payment result | `NOTIFY_FINAL_PAYMENT_RESULT` | Responder |
| 推定退款成功通知 | notify | `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS` | Responder |

> Alipay 列暂为 TODO。

## 关键 API 行为说明

- `SCAN_CODE_FOR_PAYMENT`：创建交易并发起支付，关键字段含义见 [[pix-wechat-qa-notes]]（如 `PyerTrxTrmNo`、`BizTp`、`TrxDtTm`、`ClbckUrl`、`PrmtInf`）。
- `NOTIFY_PAYMENT_RESULT`：可能返回失败；同时用于通知 trade close 或 failure。
- `QUERY_PAYMENT_ORDER_INFO`：含 `PyerIDTp`、`PyerIDNo` 等字段（必填性待确认）。
- `REFUND`：仅同步响应，无异步通知；微信会在 10 分钟内通过 `QUERY_REFUND_ORDER_INFO` 查询退款状态；超时后调用 `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS` 进行退款推定。允许 refund 失败。
- `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS`：经过多次查询、长时间（10 分钟）无结果后才会执行推定，默认仅推定通知 1 次；一旦推定，按退款成功处理，钱包可通过次日账单获得推定交易记录。

相关端到端流程见 [[flow_pix_wechat_mpc_payment]]、[[flow_pix_wechat_refund]]、[[flow_pix_wechat_reconciliation]]。

## Wechat 配置项

PIX 接入微信渠道所需的渠道级配置：

| 配置项 | 字段 | UAT Value | PROD Value |
| --- | --- | --- | --- |
| 账户机构标识 | `PyerAcctIssrId` | TODO | TODO |
| 收单机构标识 | `PyeeAcctIssrId` | TODO | TODO |
| 移动应用标识 | `AppId` | TODO | TODO |

说明：
- `PyerAcctIssrId`（Account institution identifier）：付款方账户机构标识。
- `PyeeAcctIssrId`（Acquirer institution identifier）：收单机构标识。
- `AppId`（Mobile application identifier）：移动应用标识。

汇率与利润相关配置（Rate Margin Percent 等）见 [[pix-wechat-rate-sync]]。
