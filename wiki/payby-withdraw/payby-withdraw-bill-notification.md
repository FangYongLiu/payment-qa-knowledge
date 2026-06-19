---
title: 提现账单与通知状态
domain: withdraw-cash
kind: wiki_page
slug: payby-withdraw-bill-notification
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/124289192
tags: []
---

# 提现账单与通知状态

本页梳理 PayBy 提现到银行卡在不同业务状态下，对用户发出的通知文案与账单文案的对应关系，以及提现结果页轮询行为。

## 状态-通知-账单 对应表

| 状态 | 通知 | 账单 |
|---|---|---|
| 提现提交 | Processing | Processing |
| 提现成功 | Success | Transaction complete |
| 提现失败 | Transfer Failed | Transfer Failed |
| 退票 | 无通知 | Declined by Your Bank |

## 关键说明

- **退票**：仅账单状态更新为 `Declined by Your Bank`，**不向用户发送通知**。
- **提现失败**：通知与账单同步更新为 `Transfer Failed`，资金原路退款，但不会生成独立的退款订单。
- **提现成功**：账单文案为 `Transaction complete`，与通知文案 `Success` 不同名。

## 结果页轮询

- 提现提交后，结果页**每 10 秒定时轮询一次**。
- 中间态包含：提现提交（Processing）→ 提现已提交至银行渠道。
- **成功 / 失败状态不再轮询**。

## 相关业务场景

- 银行返回成功 → 通知 + 账单更新为成功态。
- 银行返回失败 → 通知 + 账单更新为失败态，原路退款，无退款订单。
- 银行成功后退票 → 仅账单更新为 `Declined by Your Bank`，无通知。

---

相关页面：[[payby-withdraw-overview]]、[[payby-withdraw-page-rules]]、[[payby-withdraw-limits-fees]]、[[flow_payby_withdraw_to_bank]]、[[scn_payby_withdraw_core_cases]]。
