---
id: svc_payment
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp006
name: payment
dev_owner: Dewen.Li
aliases: [gp006_payment]
related_services: [svc_dpm_manager, svc_cmf, svc_counter, svc_pfs_payment, svc_member]
related_tables: []
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_online_business_direct_pay, scn_online_business_merchant_payout, scn_online_business_merchant_split, scn_online_business_pre_auth, scn_remittance_cross_border, scn_wallet_consumer_pay, scn_wallet_deposit, scn_wallet_p2p, scn_wallet_withdraw]
---

# payment

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp006` · domain=`payment-core`。

## 作用
支付中台 —— 支付指令处理，编排 dpm（记账）/cmf（渠道）/pfs（履约）/counter

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_dpm_manager]] dpm-manager（账务平台管理） · 1345693 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 482556 次 · high
- [[svc_counter]] counter（账务记账） · 240539 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 214740 次 · high
- [[svc_member]] member（会员 / 账户核心） · 52669 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
pfs-payment

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_payby_payment_create_order]] PayBy创建支付订单接口
**读写的表:** [[tbl_grc_t_payment_event]] GRC支付事件表 t_payment_event_<yyyy>

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp006` · domain=`payment-core`。
