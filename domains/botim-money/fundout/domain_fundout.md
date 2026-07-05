---
id: domain_fundout
object_type: Domain
name: fundout
aliases: [出款, 提现出款]
domain: fundout
business_line: botim-money
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
dev_owner: cong.zhou
last_reviewed_at: '2026-06-26'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [fundout, 出款]
related_services: [svc_fundout]
---

# fundout(出款)

> 域入口。平台侧资金出款。owner xiaoyan.zhou / 研发 Payment Core 团队(Cong Zhou)。

## 概述
资金出款处理:出款订单、批次、资金准备与补偿。归 Payment Core 团队;商户侧出款(merchant-fundout)另属 [[domain_merchant_management]]。

## 本域内容
- **service/** — fundout。
- **table/** — fundout(批次订单/资金准备/补偿事件等)。

## 相邻域
汇款/转账出款 → [[domain_remittance]];入款/虚拟账户 → [[domain_deposit_vam]];清结算 → [[domain_settlement]]。

## 参考索引(补)
- [[reference_payby_cash_out_overview]](Cash Out 业务总览)· [[reference_payby_withdrawal_overview]](提现流程总览)· [[reference_withdraw_to_bank_overview]](提现到银行卡)
