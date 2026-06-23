---
title: Send Money vs 手机号转账业务对比
domain: remittance
kind: wiki_page
slug: send-money-vs-phone-transfer
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/185794690
tags: []
---

# Send Money vs 手机号转账业务对比

本页对比 Send Money 与手机号转账在资金流、领取、退款、通知四个维度的差异。相关需求点参见 [[send-money-feature-requirements]]，端到端流程见 [[flow_send_money]]。

## 付款资金流

| 场景 | 手机号转账 | Send Money |
| --- | --- | --- |
| 收款人已 KYC | 付款人 → 付款人中间户 → 收款人 | 付款人（自动结算）→ 收款人 |
| 收款人未 KYC | 付款人 → 付款人中间户 → 收款人 | 付款人（手动结算）→ 收款人 |

- 手机号转账统一通过付款人中间户中转。
- Send Money 直接在付款人与收款人之间结算，按收款人 KYC 状态区分自动/手动结算。

## 领取流程

**收款人已 KYC**
- 手机号转账：接收通知付款成功后，调用 transfer 结算，存在失败可能。
- Send Money：付款时直接自动结算给收款人。

**收款人未 KYC**
- 手机号转账：通过公众号通知存在转账，KYC 完成后需用户手动领取。
- Send Money：通过聊天气泡通知存在转账，KYC 完成后系统自动结算领取（仍有结算失败可能）。

## 退款机制

| 场景 | 手机号转账 | Send Money |
| --- | --- | --- |
| 收款人未 KYC | 24H 退款，发送公众号通知 | 72H 退款，发送聊天气泡通知 |
| 收款人已 KYC | 自动领取失败时 24H 退款 | 只会出现支付失败 |

## 通知方式（自动结算成功）

- **手机号转账**
  - 付款方：付款公众号通知
  - 收款方：收款成功短信 + 公众号通知
- **Send Money**
  - 付款方：转账成功聊天气泡通知
  - 收款方：转账到账聊天气泡通知

## 关键差异小结

- 资金路径：手机号转账经中间户中转；Send Money 点对点结算。
- 未 KYC 领取：手机号转账需用户手动领取；Send Money 由系统自动结算。
- 退款时效：未 KYC 场景下手机号转账 24H、Send Money 72H。
- 通知载体：手机号转账以公众号/短信为主；Send Money 全程使用聊天气泡通知。
