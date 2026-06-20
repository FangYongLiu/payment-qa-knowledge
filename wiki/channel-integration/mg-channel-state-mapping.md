---
title: MG渠道订单状态映射表
domain: channel-integration
kind: wiki_page
slug: mg-channel-state-mapping
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:fe1a186f-8431-44b0-a534-d392e3341e7b
tags: []
---

# MG渠道订单状态映射表

本页整理 PayBy 内部订单状态（state / sub state）与 MG 渠道状态（MG state / sub state）之间的映射关系，以及在 App 账单和 Admin Portal 上的展示文案。相关渠道背景见 [[mg-channel-overview]]，特殊业务规则见 [[mg-channel-special-rules]]。

## 映射总览说明

- MG 渠道**没有 sub state**，因此映射中 MG state 与 MG sub state 设置为相同值。
- 映射用于支撑订单状态同步、退款触发与前端/后台展示三类场景。
- Admin Portal 展示文案存在"修改前 / 修改后"两套，需以修改后为准。

## 状态映射表

| PayBy state | PayBy sub state | MG state | MG sub state | Memo | App 账单展示 | Admin Portal（修改前） | Admin Portal（修改后） |
|---|---|---|---|---|---|---|---|
| WP | RRS (REMITTANCE_REQUEST_SUCCESS) | UNCOMMITTED | UNCOMMITTED | — | — | — | — |
| PS | CRS (CHANNEL_REMITTANCE_SUBMITED) | AVAIL | AVAIL | — | Processing - Transaction in progress | Submitted | Processing |
| P | CRA (CHANNEL_REMITTANCE_AUDIT) | PRCSS | PRCSS | MG 新增，被风控 | Transaction on hold | Processing - Additional Info Needed | AML Pending - Additional Info Needed |
| S | CRC (CHANNEL_REMITTANCE_COMPLETED) | RECVD | RECVD | — | Completed | Completed | Completed |
| P | CRR (CHANNEL_REMITTANCE_REJECT) | AFR | AFR | 调整为 CRR，被风控后审核拒绝，此状态只能发起撤销或退款 | Transaction on hold | Processing - Available for refund | AML Pending - Available for refund |
| F | CCR (CHANNEL_CANCEL_REMITTANCE) | CANCL | CANCL | — | Transaction Cancelled | Transaction Cancelled | Transaction Cancelled |
| F | CR (CHANNEL_REFUNDED) | REFND | REFND | MG 新增，已退款 | Transaction Failed | Transaction Failed | Transaction Failed |
| F | OC (ORDER_CLOSE) | - | - | PayBy 关闭未支付订单 / 汇款被风控失败 | — | — | — |
| F | SF (SUBMIT_FAIL) | - | - | 提交渠道失败 | — | — | — |
| CP | * | - | - | 用户 / 运营 / 系统发起的撤销，防止接口未知异常等场景 | — | — | — |
| C | CCR (CHANNEL_CANCEL_REMITTANCE) → CR (CHANNEL_REFUNDED) | - | - | 用户 / 运营主动撤销 | Transaction Failed | — | — |
| RS | PUE (PICK_UP_EXPIRE) | - | - | PayBy 检测超过 90 天未领取 | Transaction Failed | — | — |

## 关键状态说明

### PRCSS（风控中）
- 由 PayBy 的 `P / CRA` 映射而来。
- MG 端要求用户主动提交补充信息，前端已实现该交互流程。
- 关联场景：[[scn_mg_prcss_risk_review]]。

### AFR（可退款）
- 由 PayBy 的 `P / CRR` 映射而来，表示被风控后审核拒绝。
- 仅可发起撤销或退款；查询到此状态会直接触发主动退款（`SendReversal`）。

### REFND（已退款）
- 对应 PayBy `F / CR`，表示渠道侧已完成退款。
- 注意：MG 成功订单后续仍可能转为退款，需通过 customer 订单详情页的 **refresh** 按钮重新查询同步。

### PUE（PICK_UP_EXPIRE）
- 表示收款人 90 天未领取，MG 内部会将订单置为过期。
- PayBy 查询时返回 `Error=707, Message=Please call MoneyGram customer service center to complete this transaction (code 45)`。
- 处理方案：将订单挂起为 `RS / PUE`，继续轮询同步；若 MG 已退款则 PayBy 同步退款，否则保持挂起。

## 端到端流程关联

完整的下单、查询、退款链路参见 [[flow_mg_remittance]]。
