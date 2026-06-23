---
id: flow_wallet_send_money_kyc_settle
object_type: Flow
domain: fund-out-transfer
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_image
source_ref: wiki_image:cfb696a6-bf32-48ff-bc71-76d13750a4fb
tags:
- wallet
- send-money
- kyc
- settle
subdomain: null
module: null
sensitivity: normal
name: Wallet Send Money KYC完成后结算端到端流程
aliases: []
related_services:
- cgs
- transfer
- kyc
- tradeii
- pns
related_tables: []
related_scenarios:
- wallet-send-money-kyc-settle-flow
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Wallet Send Money 场景下，Payee 完成 KYC 后由 transfer 触发手工结算，经 tradeii 完成结算并更新订单，pns 推送消息通知 Payee 自动到账，Payee 通过 `/wallet/transfer/v1/get-result` 查询最终转账结果的端到端流程。

## 步骤(跨系统)
1. Payee → cgs：`1: Complete KYC`
2. cgs → kyc：`1.1: Complete KYC`
3. kyc → cgs：`1.2:` (返回)
4. cgs → Payee：`1.3:` (返回)
5. kyc → transfer：`2: Notice KYC completed`
6. transfer → tradeii：`2.1: Manual settle`
7. tradeii → transfer：`2.2: Settled` (返回)
8. transfer → transfer：`2.3: Update order` (内部自调用)
9. transfer → pns：`2.4: Message window notification`
10. pns → Payee：`2.4.1: Auto received`
11. Payee → cgs：`3: /wallet/transfer/v1/get-result`
12. cgs → transfer：`3.1:`
13. transfer → cgs：`3.2:` (返回)
14. cgs → Payee：`3.3: Transfer result` (返回)

## 涉及服务/表
- 服务：cgs、transfer、kyc、tradeii、pns
- 接口：`/wallet/transfer/v1/get-result`

## 校验点
- KYC 完成后 kyc 必须主动通知 transfer (`Notice KYC completed`)，触发后续结算
- transfer 调用 tradeii 执行 `Manual settle`，收到 `Settled` 回执后才执行 `Update order`
- 订单更新后由 transfer 经 pns 下发 `Message window notification`，Payee 端表现为 `Auto received`
- Payee 通过 `/wallet/transfer/v1/get-result` 查询结果，链路 cgs → transfer 返回 `Transfer result`

</result>
