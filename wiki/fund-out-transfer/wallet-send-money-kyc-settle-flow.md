---
title: Wallet Send Money - 收款人KYC完成后自动结算流程
domain: fund-out-transfer
kind: wiki_page
slug: wallet-send-money-kyc-settle-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:cfb696a6-bf32-48ff-bc71-76d13750a4fb
tags: []
---

# Wallet Send Money - 收款人KYC完成后自动结算流程

本页描述 Payee 完成 KYC 后，由 kyc 服务通知 transfer 触发手工结算、订单更新、消息通知与结果查询的端到端时序。相关时序图见 [[flow_wallet_send_money_kyc_settle]]。

## 参与方

- Payee（收款人）
- cgs
- transfer
- kyc
- tradeii
- pns

## 阶段 1：Payee 完成 KYC

- `1` Payee → cgs：Complete KYC
- `1.1` cgs → kyc：Complete KYC
- `1.2` kyc → cgs：返回
- `1.3` cgs → Payee：返回

## 阶段 2：KYC 完成通知与自动结算

- `2` kyc → transfer：Notice KYC completed
- `2.1` transfer → tradeii：Manual settle（手工结算）
- `2.2` tradeii → transfer：Settled
- `2.3` transfer → transfer：Update order（更新订单）
- `2.4` transfer → pns：Message window notification
- `2.4.1` pns → Payee：Auto received（自动收款通知）

## 阶段 3：查询转账结果

- `3` Payee → cgs：`/wallet/transfer/v1/get-result`
- `3.1` cgs → transfer：转发查询
- `3.2` transfer → cgs：返回
- `3.3` cgs → Payee：Transfer result
