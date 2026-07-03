---
id: svc_pfs_payment
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp014
name: pfs-payment
dev_owner: Dewen.Li
aliases: [gp014_pfs-payment]
related_services: [svc_dpm_manager, svc_member, svc_payment]
related_tables: []
related_scenarios: [scn_online_business_direct_pay, scn_online_business_merchant_split, scn_wallet_withdraw]
---

# pfs-payment

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp014` · domain=`payment-core`。

## 作用
支付履约 / 清分（Payment Fulfillment，enterMulti），被 trade/payment/offline/vis 调用

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_dpm_manager]] dpm-manager（账务平台管理） · 10290661 次 · high
- [[svc_member]] member（会员 / 账户核心） · 8303794 次 · med·待核实
- [[svc_payment]] payment（支付中台） · 6310579 次 · high

**被调用(上游)—— 这些服务调用本服务:**
offline-payment, vis, payment, tradeii, fundout, reconciliation

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）

## 关键方法 / 入口
enterMulti

## 涉及的 API / 数据库表
- **暴露/相关 API**:Dubbo `enterMulti`(多方清分入口)、`QuickPayPaymentRequest`、`RefundPaymentRequest`(退款);被 [[svc_tradeii]]/[[svc_payment]]/fundout/reconciliation 调。
- **读写的表**:清分 / 业务状态流水(待补具体表)。

## 关键方法 / 入口(UAT 实测)
- `enterMulti`(清分);`QuickPayPaymentRequest`(快捷支付履约);退款 `RefundPaymentRequest`。
- **业务状态机 BSS/PSS**:`PSS:PaySubmit->Paying`(支付中)→ `BSS:PaySubmit->Paid`(已支付);退款 `BSS:Init->RefundSubmit->Refunded`。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **状态推进**:支付成功后 pfs 监听 `PaymentResponse` 把业务状态推 `Paid`;卡在 `Paying` 说明履约/记账未回。
- **清分**:tradeii `enterMulti` 发起 → 下沉 [[svc_payment]] + [[svc_dpm_manager]] 记账;退款走反向清分。
- **怎么测/定位**:按支付凭证号(`pay_voucher_no` 311…)跟 BSS 状态流转;成功链应见 `PaySubmit->Paying->Paid`。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_direct_pay]](自动化:直连支付自动化)
- [[auto_online_business_merchant_split]](自动化:商户分账自动化)
- [[auto_wallet_withdraw]](自动化:钱包提现自动化)
- [[flow_botim_transfer]](流程:BOTIM/ToC 转账与加款端到端流程)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_payby_cash_out]](流程:现金提现端到端流程 (Cash Out / Withdraw Cash via POS))
- [[flow_payby_withdraw_to_bank]](流程:提现到银行卡端到端流程 (Transfer to Bank Account / IBAN / Aani))
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_merchant_split]](场景:商户分账 (Merchant Split))
- [[scn_wallet_withdraw]](场景:钱包提现 (Withdraw))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp014` · domain=`payment-core`。
