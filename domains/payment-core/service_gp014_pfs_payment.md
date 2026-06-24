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
- **暴露/相关 API**:待补
- **读写的表**:待补

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`pfs-payment`):
- ERROR 1532075 次,主要:`PaymentProcessService`×1531985、`DefaultOrderQueryFacade`×90
- WARN 292 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp014` · domain=`payment-core`。
