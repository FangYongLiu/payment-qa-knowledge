---
id: svc_cards
object_type: Service
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp093
name: cards
dev_owner: Qian.Wang
aliases: [gp093_cards]
related_services: []
related_tables: []
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_online_business_direct_pay, scn_online_business_merchant_payout, scn_online_business_pre_auth, scn_wallet_deposit]
---

# cards

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp093` · domain=`card`。

## 作用
卡管理 —— 绑卡 / 卡 token（被收单 / 收银 / 渠道广泛调用）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`card`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend, tradeii, cashierii, cashdesk-api, qpay-mpgs, fundout

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp093` · domain=`card`。
