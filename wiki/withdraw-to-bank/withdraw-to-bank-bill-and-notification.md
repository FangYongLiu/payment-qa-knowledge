---
title: 提现账单与通知状态映射
domain: withdraw-to-bank
kind: wiki_page
slug: withdraw-to-bank-bill-and-notification
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:bc1e3b1d-5f33-4288-87a2-3ca7a3a28ca7
tags: []
---

# 提现账单与通知状态映射

本页梳理 Transfer to Bank Account 业务在四种关键状态下，用户端收到的通知文案与账单（Bill）展示文案的对应关系。

## 状态映射表

| 状态 | 通知 | 账单 |
| --- | --- | --- |
| 提现提交 | Processing | Processing |
| 提现成功 | Success | Transaction complete |
| 提现失败 | Transfer Failed | Transfer Failed |
| 退票 | 无通知 | Declined by Your Bank |

## 状态说明

- **提现提交**：用户在提现页提交订单后立即触发，通知与账单同步进入 `Processing`。
- **提现成功**：银行返回成功，通知文案为 `Success`，账单更新为 `Transaction complete`。
- **提现失败**：银行返回失败，通知为 `Transfer Failed`，账单同步为 `Transfer Failed`；资金原路退款，且不生成单独的退款订单。
- **退票**：银行成功后发生退票，**不向用户发送通知**，仅账单状态更新为 `Declined by Your Bank`。

## 关联说明

- 结果页的轮询逻辑（每 10 秒一次，成功/失败状态不再轮询）见 [[withdraw-to-bank-page-rules]]。
- 业务整体流程与各状态的触发时机见 [[withdraw-to-bank-overview]]。
- 状态流转的验证方法（含通过 basis、counter 管理置结果）见 [[withdraw-to-bank-test-guide]]。
