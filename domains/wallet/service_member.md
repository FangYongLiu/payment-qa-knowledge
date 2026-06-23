---
id: svc_member
object_type: Service
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp005
name: member
dev_owner: 陆亚东
aliases: [gp005_member]
related_services: [svc_dpm_accounting, svc_ccdpm_accounting, svc_cms]
related_tables: []
---

# member

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp005` · domain=`wallet`。

## 作用
会员 / 账户核心 —— 开户 / 查账户 / 校验支付密码 / 受益人（openAccount/checkPassword/queryAccountById），下游 dpm-accounting

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`wallet`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_dpm_accounting]] dpm-accounting（账务平台记账） · 10913 次 · high
- [[svc_ccdpm_accounting]] ccdpm-accounting（加密货币账务记账） · 607 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 26 次 · high

**被调用(上游)—— 这些服务调用本服务:**
remittance, pfs-payment, reconciliation, credit-business, merchant-frontend, tradeii

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）
- §7. 跨境汇款（toC，`test_remittance`）
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）

## 观测到的对外方法
queryAccountById, queryMemberIntegratedInfo, openAccount, queryAccountByMemberId, checkPassword, queryBeneficiaryConfig
