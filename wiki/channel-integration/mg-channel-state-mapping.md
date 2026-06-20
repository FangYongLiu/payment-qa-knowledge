---
title: MG渠道订单状态映射表
domain: channel-integration
kind: wiki_page
slug: mg-channel-state-mapping
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1268547712
tags: []
---

# MG渠道订单状态映射表

本页说明 MG (MoneyGram) 渠道订单在 PayBy 系统内的 state / sub state 与 MG 自身 state / sub state 之间的映射关系，以及在 App 账单和 Admin Portal 上的 UI 展示文案。渠道整体接入说明见 [[mg-channel-overview]]。

## 基本规则

- MG 自身没有 sub state，因此映射时 **MG state 与 MG sub state 设置为相同值**。
- 状态推进主要由 [[api_mg_order_status_query]] 轮询驱动，MG 不提供主动回调。
- 退款由 [[api_mg_send_reversal]] 触发。

## 状态映射表

| PayBy state | PayBy sub state | MG state / sub state | Memo | App 账单展示 | Admin Portal (修改前) | Admin Portal (修改后) |
|---|---|---|---|---|---|---|
| WP | RRS (REMITTANCE_REQUEST_SUCCESS) | UNCOMMITTED | — | — | — | — |
| PS | CRS (CHANNEL_REMITTANCE_SUBMITED) | AVAIL | — | Processing - Transaction in progress | Submitted | Processing |
| P | CRA (CHANNEL_REMITTANCE_AUDIT) | PRCSS | MG 新增，被风控 | Transaction on hold | Processing - Additional Info Needed | AML Pending - Additional Info Needed |
| S | CRC (CHANNEL_REMITTANCE_COMPLETED) | RECVD | — | Completed | Completed | Completed |
| P | CRR (CHANNEL_REMITTANCE_REJECT) | AFR | 调整为 CRR，被风控后审核拒绝，此状态只能发起撤销或退款 | Transaction on hold | Processing - Available for refund | AML Pending - Available for refund |
| F | CCR (CHANNEL_CANCEL_REMITTANCE) | CANCL | — | Transaction Cancelled | Transaction Cancelled | Transaction Cancelled |
| F | CR (CHANNEL_REFUNDED) | REFND | MG 新增，已退款 | Transaction Failed | Transaction Failed | Transaction Failed |
| F | OC (ORDER_CLOSE) | - | PayBy 关闭未支付订单 / 汇款被风控失败 | — | — | — |
| F | SF (SUBMIT_FAIL) | - | 提交渠道失败 | — | — | — |
| CP | * | - | 用户 / 运营 / 系统发起的撤销，防止接口未知异常等场景 | — | — | — |
| C | CCR (CHANNEL_CANCEL_REMITTANCE) → CR (CHANNEL_REFUNDED) | - | 用户 / 运营主动撤销 | Transaction Failed | — | — |
| RS | PUE (PICK_UP_EXPIRE) | - | PayBy 检测超过 90 天未领取 | Transaction Failed | — | — |

## 关键状态说明

### PRCSS（渠道审核中）
- MG 风控触发，要求用户主动补充信息。
- 前端已实现补充信息流程。
- 复现方法：使用印度 bank transfer 渠道，填写 First Name: `Buggs`, Last Name: `Bunny`，下单后几分钟订单会自动变为 PRCSS。

### AFR（可退款状态）
- 被风控后审核拒绝。
- 查询到该状态可直接发起主动退款（调用 [[api_mg_send_reversal]]）。

### REFND（已退款）
- MG 渠道订单成功之后仍可能失败转退款。
- 因此 customer 订单详情页对 MG 的成功订单提供 **Refresh 按钮**，点击会触发订单状态查询；若结果变为 refund，则 PayBy 系统也对该笔交易执行退款。

### RS / PUE（PICK_UP_EXPIRE）
- 含义：90 天收款人未领取，MG 内部将订单置为过期。
- PayBy 查询时返回 `Error=707, Message=Please call MoneyGram customer service center to complete this transaction (code 45)`。
- 处理方案：
  - 查询返回 Error = 707 时，将订单挂起为 RS (REMITTANCE_SUSPEND)，子状态 PUE (PICK_UP_EXPIRE)。
  - 挂起订单继续轮询同步状态：若变为已退款，PayBy 同步执行退款（是否有对应对账单待确认）；否则继续挂起。
  - 此场景下退款后的状态为「已退款」（待验证）。

## 注意事项

- 状态查询与状态推进的接口契约见 [[api_mg_order_status_query]]。
- 主动退款触发条件（cancel 按钮 / 超 60 天未成功的 cash pickup / AFR）详见 [[api_mg_send_reversal]]。
- App 账单与 Admin Portal 文案存在「修改前 / 修改后」两套版本，以表格列为准。
