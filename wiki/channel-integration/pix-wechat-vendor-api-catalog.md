---
title: 微信渠道Vendor API清单与场景映射
domain: channel-integration
kind: wiki_page
slug: pix-wechat-vendor-api-catalog
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: []
---

# 微信渠道Vendor API清单与场景映射

本页梳理微信MPC渠道接入中各业务场景与Vendor API（Requester / Responder）的对应关系，并附关键字段与行为说明。总体接入背景见 [[pix-wechat-mpc-integration-overview]]。

## 场景与API映射总表

| 场景 | 微信Vendor API | 角色 |
|---|---|---|
| 解析二维码 | `/pix/mpc/v1/parse`（QUERY_MERCHANT_CODE） | Requester |
| 创建交易/扫码支付 | `/pix/mpc/v1/create-trade`（SCAN_CODE_FOR_PAYMENT） | Requester |
| 处理交易结果 | NOTIFY_PAYMENT_RESULT | Requester |
| 退款 | REFUND | Responder |
| 关闭支付 | CLOSE_PAYMENT | Responder |
| 查询支付 | QUERY_PAYMENT_ORDER_INFO | Responder |
| 查询退款 | QUERY_REFUND_ORDER_INFO | Responder |
| 下载对账文件 | QUERY_BILL_ADDRESS | Requester |
| 通知最终支付结果 | NOTIFY_FINAL_PAYMENT_RESULT | Responder |
| 退款推定通知 | NOTIFY_PRESUPPTIVE_REFUND_SUCCESS | Responder |

## 扫码与下单

- `/pix/mpc/v1/parse`：调用 vendor 获取商户信息，将商户码信息（含费率信息）落 ES。
- `/pix/mpc/v1/create-trade`：从 ES 取商户码信息，在 vendor 创建交易订单，生成收银台 trade order 并返回 `cashierUrl`，需按费率校验金额。
- 端到端时序见 [[flow_pix_wechat_mpc_payment]]，费率来源见 [[pix-wechat-rate-sync]]。

## 支付结果通知

- `NOTIFY_PAYMENT_RESULT`：处理交易结果通知，触发：
  - 通知 vendor 支付结果
  - 调用 query 落账单（bill）
  - 调用 reconciliation 保存 fundout glide
- 该接口可能返回失败；交易关闭或失败也会通过此接口通知。
- `instOrderNo` 来自 tradeii，文档关键字 `DbtrBankId`。

## 最终支付结果

- `NOTIFY_FINAL_PAYMENT_RESULT`（Responder）：若最终支付失败，触发退款交易处理。

## 退款

- `REFUND`（Responder）：仅同步响应，无异步通知。
  - 必要校验后异步请求退款，返回 vendor 成功。
  - 通知退款 bill。
  - 退款支付金额计算：`Refund pay amount = Refund transaction amount / Original transaction amount * Original pay amount`
  - 允许退款失败。
- `QUERY_REFUND_ORDER_INFO`（Responder）：微信会在 10 分钟内通过该接口查询退款状态。
- `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS`（Responder）：退款推定通知。
  - 触发条件：经过多次查询及约 10 分钟未得结果后执行推定。
  - 默认只推定通知 1 次，一旦推定即按退款成功处理。
  - 钱包可通过次日账单获得推定的交易记录。
- 详细流程见 [[flow_pix_wechat_refund]]。

## 关闭支付

- `CLOSE_PAYMENT`（Responder）：关闭交易，需注意微信特有的关闭逻辑。

## 查询类

- `QUERY_PAYMENT_ORDER_INFO`（Responder）：查询本地交易状态。
- `QUERY_REFUND_ORDER_INFO`（Responder）：查询退款状态（亦用于退款推定流程中的轮询）。

## 对账文件下载

- `QUERY_BILL_ADDRESS`（Requester）：通过 vendor 接口下载对账文件，经 ufs 保存，将 `fileTag` 落库；reconciliation 通过 dubbo api 获取 `fileTag` 后做自动对账。
- 详见 [[flow_pix_wechat_reconciliation]]。

## 关键字段说明（节选）

`SCAN_CODE_FOR_PAYMENT`：

- `PyerTrxTrmNo`：Payer terminal code，即 Device Id
- `BizTp`：Business type，来自 `QUERY_MERCHANT_CODE`
- `TrxDtTm`：交易日期，须与 `TrxId` 日期一致
- `ClbckUrl`：账户机构回调收单机构的 URL
- `PrmtInf`：营销信息

`QUERY_PAYMENT_ORDER_INFO`：

- `PyerIDTp` / `PyerIDNo`：是否必填待确认

更多字段答疑见 [[pix-wechat-qa-notes]]，配置项见 [[pix-wechat-configuration]]。
