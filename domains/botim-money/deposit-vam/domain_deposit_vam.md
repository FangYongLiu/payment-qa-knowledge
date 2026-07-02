---
id: domain_deposit_vam
object_type: Domain
name: deposit-vam
aliases: [fund-inflow, VAM, 资金入款, 虚拟账户, IBAN]
domain: deposit-vam
business_line: botim-money
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
dev_owner: cong.zhou
last_reviewed_at: '2026-06-26'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [deposit-vam, 资金入款, 虚拟账户, IBAN]
related_services: [svc_deposit, svc_vis, svc_visii, svc_vcs, svc_escrow, svc_escrowii]
---

# deposit-vam(资金入款 / 虚拟账户)

> 域入口。多渠道充值入款 + 虚拟账户管理。owner xiaoyan.zhou / 研发 Payment Core 团队(Cong Zhou)。

## 概述
- **入款(Deposit)** — 多渠道钱包充值(银行转账、卡、Aani、现金、Apple/Google Pay)。
- **虚拟账户(VAM)** — vis(FAB 虚拟账户)、**visii(Zand 虚拟账户,含 IBAN 创建)**、vcs(FAB 虚拟卡)、escrow/escrowii(托管账户)。

## 本域内容
- **service/** — deposit、vis、visii、vcs、escrow、escrowii。
- **table/** — vis(虚拟账户/通知流水)。
- **api/**(1)— vam 入款通知。

## 相邻域
出款 → [[domain_fundout]];渠道 → [[domain_payment_tool]];清结算 → [[domain_settlement]];钱包 → [[domain_wallet]]。
