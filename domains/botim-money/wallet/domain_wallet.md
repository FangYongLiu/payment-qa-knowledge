---
id: domain_wallet
object_type: Domain
name: wallet
aliases: [钱包]
domain: wallet
business_line: botim-money
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [wallet, 钱包]
related_services: [svc_push_to_pay, svc_pus, svc_household, svc_member_task, svc_gold_wallet, svc_pqs]
---

# wallet(钱包)

> 业务域总览(入口节点)。owner qianlong.wang。细节见各服务对象。

## 概述
钱包域:push-to-pay、pus、household、促销(promo)、pqs 等钱包相关能力。

## 覆盖范围
共 6 个服务:push-to-pay、pus、household、member-task、gold-wallet、pqs。

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[auto_wallet_AA_splitting]](自动化:AA 收款自动化)
- [[auto_wallet_deposit]](自动化:钱包充值自动化)
- [[auto_wallet_friend_transfer]](自动化:好友转账自动化)
- [[auto_wallet_payment_code]](自动化:付款码自动化)
- [[auto_wallet_phoneTransfer]](自动化:手机号转账自动化)
- [[auto_wallet_ppcTransaction]](自动化:PPC 交易自动化)
- [[auto_wallet_red_pkg]](自动化:红包自动化)
- [[auto_wallet_vis_iban_retry_job]](自动化:vis_ibanAccountRetryJob 批次处理任务 (VAM IBAN 申请重试 Job))
- [[auto_wallet_withdraw]](自动化:钱包提现自动化)
- [[flow_payby_cash_in]](流程:现金充值流程 (Cash In via POS))
- [[flow_payby_cash_out]](流程:现金提现端到端流程 (Cash Out / Withdraw Cash via POS))
- [[flow_payby_withdraw_to_bank]](流程:提现到银行卡端到端流程 (Transfer to Bank Account / IBAN / Aani))
- [[scn_wallet_consumer_pay]](场景:消费者付款 (Payment Code / PPC))
- [[scn_wallet_deposit]](场景:钱包充值 (Deposit / Top-Up))
- [[scn_wallet_p2p]](场景:钱包 P2P 转账 / 红包 (Transfer & Red Packet))
- [[scn_wallet_vam_iban_apply_activate]](场景:VAM IBAN 虚拟账户申请激活与交易通知 (VAM IBAN Apply / Activate / Notify))
- [[scn_wallet_withdraw]](场景:钱包提现 (Withdraw))
- [[scn_wallet_withdraw_to_bank]](场景:提现到银行卡场景 (Transfer to Bank Account 字段/状态/限额/测试))
