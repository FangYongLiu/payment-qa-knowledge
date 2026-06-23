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
dev_owner: 李德文
aliases: [gp006_payment]
related_services: [svc_dpm_manager, svc_cmf, svc_pfs_payment, svc_counter, svc_member]
related_tables: []
---

# payment

> 来源:UAT Kibana trace 观测(2026-06-22~23 UAT cgs 回归窗口,真实但非穷尽)+ 作用说明。候选待人审。app_group=`gp006` · domain=`payment-core`。

## 作用
支付中台 —— 支付指令处理，编排 dpm（记账）/cmf（渠道）/pfs（履约）/counter

## 系统中的位置
- 功能层:交易 / 支付中台 (Trade / Payment Core)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖这些服务完成处理:**
- [[svc_dpm_manager]] dpm-manager（账务平台管理） · 2653 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 999 次 · high
- [[svc_pfs_payment]] pfs-payment（支付履约 / 清分） · 536 次 · high
- [[svc_counter]] counter（账务记账） · 456 次 · high
- [[svc_member]] member（会员 / 账户核心） · 78 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
pfs-payment

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
