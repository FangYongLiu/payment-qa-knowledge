---
title: Send Money 与手机号转账对比
domain: remittance
kind: wiki_page
slug: send-money-vs-phone-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:77b3f2a6-a8a3-4481-944a-58fb9f23fdda
tags: []
---

# Send Money 与手机号转账对比

本页对比 Send Money 与传统手机号转账在资金流、领取方式、退款机制和通知触达上的差异，便于理解两套链路的设计取舍。需求与端到端流程详见 [[wallet-send-money-redesign]] 与 [[flow_send_money]]。

## 付款资金流

按收款人 KYC 状态区分：

- **收款人已 KYC**
  - 手机号转账：付款人 → 付款人中间户 → 收款人
  - Send Money：付款人（自动结算）→ 收款人
- **收款人未 KYC**
  - 手机号转账：付款人 → 付款人中间户 → 收款人
  - Send Money：付款人（手动结算）→ 收款人

Send Money 取消了中间户环节，资金路径更短。

## 领取方式

- **收款人已 KYC**
  - 手机号转账：收款人接收通知付款成功后，调用 transfer 结算，存在失败可能
  - Send Money：付款时直接自动结算给收款人
- **收款人未 KYC**
  - 手机号转账：通过公众号通知有转账，收款人完成 KYC 后需**手动领取**
  - Send Money：通过聊天气泡通知有转账，收款人完成 KYC 后**系统自动结算领取**（仍可能结算失败）

## 退款机制

- **收款人未 KYC**
  - 手机号转账：24H 未领取退款，发送公众号通知
  - Send Money：72H 未领取退款，发送聊天气泡通知
- **收款人已 KYC**
  - 手机号转账：自动领取失败时，24H 退款
  - Send Money：仅会出现支付失败的情况（不存在领取超时退款）

## 通知机制（自动结算成功场景）

- **手机号转账**
  - 付款方：付款公众号通知
  - 收款方：收款成功短信 + 公众号通知
- **Send Money**
  - 付款方：转账成功聊天气泡通知
  - 收款方：转账到账聊天气泡通知

Send Money 的通知通道全面切换到 App 内聊天气泡，不再依赖公众号与短信。

## 关键差异小结

| 维度 | 手机号转账 | Send Money |
| --- | --- | --- |
| 中间户 | 经过付款人中间户 | 无中间户 |
| 已 KYC 领取 | 通知后调用 transfer 结算 | 自动结算 |
| 未 KYC 领取 | KYC 后手动领取 | KYC 后系统自动结算 |
| 退款时效（未 KYC） | 24H | 72H |
| 通知通道 | 公众号 / 短信 | 聊天气泡 |
