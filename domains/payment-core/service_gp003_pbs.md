---
id: svc_pbs
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp003
name: pbs
dev_owner: Yadong.Lu
aliases: [gp003_pbs]
related_services: [svc_acs]
related_tables: []
---

# pbs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp003` · domain=`payment-tools`。

## 作用
计费 / 定价（Pricing & Billing，pricingPayFee），调 acs

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`payment-tools`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 270003 次 · high

**被调用(上游)—— 这些服务调用本服务:**
fundout, offline-payment, tradeii, cashierii, cashdesk-api

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）

## 观测到的对外方法
pricingPayFee
