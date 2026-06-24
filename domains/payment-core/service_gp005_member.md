---
id: svc_member
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp005
name: member
dev_owner: Yadong.Lu
aliases: [gp005_member]
related_services: [svc_dpm_accounting, svc_ccdpm_accounting, svc_cms, svc_kyc, svc_acs, svc_pts, svc_cards]
related_tables: []
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_remittance_cross_border, scn_wallet_consumer_pay, scn_wallet_deposit, scn_wallet_p2p, scn_wallet_withdraw, scn_card_manage, scn_payment_tools_deduct_channel, scn_wallet_account_mgmt, scn_wallet_zand_iban_migration]
---

# member

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp005` · domain=`payment-core`。

## 作用
会员 / 账户核心 —— 开户 / 查账户 / 校验支付密码 / 受益人（openAccount/checkPassword/queryAccountById），下游 dpm-accounting

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_dpm_accounting]] dpm-accounting（账务平台记账） · 3401522 次 · high
- [[svc_ccdpm_accounting]] ccdpm-accounting（加密货币账务记账） · 60299 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 4806 次 · high
- [[svc_kyc]] kyc（实名认证） · 814 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 390 次 · high
- [[svc_pts]] pts · 238 次 · high
- [[svc_cards]] cards（卡管理） · 2 次 · high

**被调用(上游)—— 这些服务调用本服务:**
remittance, pfs-payment, reconciliation, credit-business, merchant-frontend, tradeii

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_payby_get_member_balance]] 查询会员余额接口、[[api_member_query_eid_bound_account]] 查询EID绑定手机账户接口、[[api_member_change_mobile_refresh_kyc]] 变更手机并刷新KYC接口
**读写的表:** [[tbl_member_tr_bank_card_token]] 银行卡签约Token表、[[tbl_member_tr_deduct_channel]] 代扣渠道表 tr_deduct_channel、[[tbl_member_db]] 会员相关库(member)核心表

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）
- §7. 跨境汇款（toC，`test_remittance`）
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）

## 关键方法 / 入口
queryAccountById, queryMemberIntegratedInfo, openAccount, queryAccountByMemberId, checkPassword, queryBeneficiaryConfig

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp005` · domain=`payment-core`。
