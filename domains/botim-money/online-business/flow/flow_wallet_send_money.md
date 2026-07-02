---
id: flow_wallet_send_money
object_type: Flow
name: Wallet Send Money 转账(KYC结算 / 过期退款)
aliases: [Wallet Send Money, Send Money, Wallet Redesign Send Money]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki_image:cfb696a6-bf32-48ff-bc71-76d13750a4fb
tags: [online-business, transfer, send-money, wallet, kyc]
related_services: [svc_cgs, svc_kyc, svc_tradeii, svc_pns]
related_tables: [tbl_transferii_t_wallet_order, tbl_transferii_t_party_order, tbl_transferii_t_order_permit]
related_scenarios: []
---

# Wallet Send Money 转账(KYC结算 / 过期退款)

## 概述
Wallet Redesign 下的 Send Money 转账能力。Payer 发起转账,收款方(Payee)完成 KYC 后系统自动结算到账;若订单在 KYC 完成前过期则触发退款。落库在 `transferii` schema(钱包订单主表 + 参与方订单 + 收款凭证 + 取消订单)。

> 注:`transfer` 转账业务服务对象未单独建(待补),正文以文字出现。用例图角色:Payer(发起 Send)、Payee(需 KYC 后收款)。

## 步骤(跨系统)
### A. 收款人 KYC 完成后自动结算
1. Payee → [[svc_cgs]]:Complete KYC → cgs → [[svc_kyc]] → 返回
2. [[svc_kyc]] → transfer(待补):Notice KYC completed
3. transfer → [[svc_tradeii]]:Manual settle(手工结算)→ 返回 Settled
4. transfer 内部:Update order(更新订单)
5. transfer → [[svc_pns]]:Message window notification → pns → Payee:Auto received(自动到账通知)
6. Payee → cgs:`/wallet/transfer/v1/get-result` → cgs → transfer → 返回 Transfer result

### B. 过期订单退款
1. transfer 自身轮询/查询过期订单(Query expired orders)
2. transfer → [[svc_tradeii]]:Initiate refund(同步)→ 返回退款结果
3. transfer 内部:Update order(更新订单状态)
4. transfer → [[svc_pns]]:Message window notice → 向 Payer 与 Payee 推送通知

### 用例关系(Send Money 用例图)
- `Send`(Payer 发起)«Include» `Notification`
- `Receive` «Include» `Notification`、`Kyc Finished`;«Extend» `Send`(扩展点 Payee KYCed)
- `Refund` «Extend» `Send`(扩展点 Expired,交易过期触发退款)
- `Transaction Detail`:Payer 与 Payee 均可查看

## 关联关系
- **经过的服务**:[[svc_cgs]]、[[svc_kyc]]、[[svc_tradeii]]、[[svc_pns]](+ transfer 待补)(= `related_services`)
- **关键表**:[[tbl_transferii_t_wallet_order]]、[[tbl_transferii_t_party_order]]、[[tbl_transferii_t_order_permit]](= `related_tables`)
- **关键场景**:待补(本流程暂无独立 Scenario 对象)

## 校验点
- KYC 完成后 [[svc_kyc]] 必须主动通知 transfer(`Notice KYC completed`)触发结算;transfer 调 tradeii `Manual settle`,收到 `Settled` 后才 `Update order`,再经 [[svc_pns]] 下发通知,Payee 端表现 `Auto received`。
- 过期退款:退款先于订单状态更新与通知;订单更新成功后才触发消息通知(Payer + Payee 双向)。
- 查询结果链路:`/wallet/transfer/v1/get-result` 经 cgs → transfer 返回 Transfer result。
- 落库:一笔 `t_wallet_order` 对应多条 `t_party_order`(数量 = `party_count`);`t_order_permit` 关联收款凭证;`t_cancel_order` 记录取消(详见各表对象)。
